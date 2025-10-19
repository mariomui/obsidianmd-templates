<%*
// based off [[,aka-macro-MUID-3118]]
// |MUID-145| Use the longform template before using MUID-145.

// # TOOLS
const {default: obs} = this.app.plugins.plugins['templater-obsidian'].templater.current_functions_object.obsidian
const getFileCache =  this.app.metadataCache.getFileCache.bind(tp);
const getFirstLinkpathDest =  this.app.metadataCache.getFirstLinkpathDest.bind(tp);

// # KNOBS
const isSilentLoggingEnabled = true;

// # HELPERS
const log = (...args) => {
	!isSilentLoggingEnabled && console.log(...args)
}

// # CONSTS & TYPES
const SORT_FRONTMATTER_CMD_ID = "obsidian-one-ring:sort frontmatter";

let FrontmatterFieldnames;
(function (FrontmatterFieldnames) {
	FrontmatterFieldnames["WORKING_TITLE"] = "WORKING_TITLE";
	FrontmatterFieldnames["LONGFORM"] = "longform";
	FrontmatterFieldnames["MUID"] = "MUID";
	FrontmatterFieldnames["PROJECT_TITLE"] = "PROJECT_TITLE";
})(
	FrontmatterFieldnames || (FrontmatterFieldnames = {})
);

// BOOTUP

tp.hooks.on_all_templates_executed(async () => {

	const fileView = tp.app.workspace.getActiveFileView()
	
	const metadataEditor = fileView.metadataEditor
	const serializeYaml = metadataEditor.serialize.bind(metadataEditor);
	const synchronizeYaml = metadataEditor.synchronize.bind(metadataEditor);
	await genMain({
      fileView, serializeYaml, metadataEditor, synchronizeYaml, checkHasFieldname, getFileCache, getFirstLinkpathDest
    })
    .catch(console.log)
})

// ## UTILS

function checkHasFieldname(fig = {}, field_name) {
	log({fig}, "checkhasFieldname")
	return !!fig?.hasOwnProperty?.call(fig, field_name);
}

// # WORKHORSE;
async function genMain(pkg) {

	// # factory-created functions that add a little timer to the actions. A stopgap (so I dont actually have to write a task runner)
  const genSynchronizeYaml = createGenFrontmatterHelper(1000)
	const genSortYaml = createGenFrontmatterHelper(1000)

	// log(this.container, "container"); templater doesn't have a container like dvjs does. window might exist.
	
	// # Setup poorman's logging
	const {$el, $frag} = await genCreateDiv(
		tp,
		{},
	);

	// # Identfying the dependencies;
  const {
      fileView, serializeYaml, metadataEditor, synchronizeYaml, checkHasFieldname
  } = pkg;

	// # Setting the table
	const fm = serializeYaml();

	const root_project_folder_note_name = fileView?.file?.parent?.parent?.parent?.name || "";
	const rootProjectTFile = tp.app.metadataCache.getFirstLinkpathDest( 
		root_project_folder_note_name
	)
	const parentFm = tp.app.metadataCache
		.getFileCache(rootProjectTFile)?.frontmatter || {};
	
	console.log({root_project_folder_note_name,parentFm})

	// # Early Exit checks
	const checkIsAllFieldnamesExist = (fm, field_names) => {
		const isAllFieldnamesExist = Object.values(
			field_names
		).every((fn) => {
			const hasFieldname = checkHasFieldname(fm, fn)
			const isFnPopulated = Boolean(fm?.[fn]);
	
			log({fn, fv: fm[fn]})
				
			let texts = []
	
			if (hasFieldname === false) {
				texts.push(`${fn} does not exist or is not! Please add!`);
				texts.push("Exiting...")
	
			} 
			if (isFnPopulated === false) {
				texts.push(`${fn} exists but has no value.`)
				texts.push("Exiting...")
			}
			const text = texts.join(" // ");
	
			if (hasFieldname === false || isFnPopulated === false) {
				const earlyExitDivInfo = {
						text,
						attr: {
							style: "background: red;padding: .5em .5em; border-radius: 5px 5px;",
						}
				}
				window.createDiv(earlyExitDivInfo, ($div) => {
					$frag.$el.replaceChildren($div)
				
					new obs.Notice(
						$frag.$el,
						2000
					);
				})
				throw new Error("Story Title must be populated for macro to work properly. Exiting...")
	
			}
			
			return hasFieldname;
		});
		return isAllFieldnamesExist;
	}
	const isParentFmFieldsAllSet = checkIsAllFieldnamesExist(
		parentFm, 
		[FrontmatterFieldnames.MUID, FrontmatterFieldnames.WORKING_TITLE]
	);
	const isIndexFmFieldsAllSet = checkIsAllFieldnamesExist(
		fm, 
		[ FrontmatterFieldnames.LONGFORM, 
		// FrontmatterFieldnames.PROJECT_TITLE, 
		]
	);
	
	if (!fm 
	|| !isParentFmFieldsAllSet || !isIndexFmFieldsAllSet
	) {
		throw new Error("not all fields exist");
		return;
	}

	// # Logic


	// ## Update the long form fig.
	const longformFig = fm[FrontmatterFieldnames.LONGFORM]

	// ## temporary update function. 
	const updateLongformFieldValue = (field_name, value) => {
		longformFig[field_name] = value;
	}

	const muid_prefixed_story_title = `${parentFm[FrontmatterFieldnames.MUID]},${parentFm[FrontmatterFieldnames.WORKING_TITLE]}`;
	// fm[FrontmatterFieldnames.STORY_TITLE]

	updateLongformFieldValue(
		"title",
		muid_prefixed_story_title
	);
	const addonFig = {
		"PROJECT_TITLE": muid_prefixed_story_title
		
	}
	// ## Pre-Sync the fig using metadataEditor. Should also update the metadataCache. 
	const updatedFm = syncFmWithUserData(
    fm,
    {...fm, "longform": longformFig, ...addonFig} // custom user data
  );
  
  const aboutToBeYaml = { ...updatedFm };

	// ## TASKS PIPELINE (Sync and then sort)
	// 🐛 firstparameter is wacky, remove someday.

  await genSynchronizeYaml(
    aboutToBeYaml,
    () => {
      synchronizeYaml(aboutToBeYaml)
    }
  ).catch((err) => {
    throw new Error(JSON.stringify({err, desc: "genSynchronizeYaml error"}))
  })

  await genSortYaml( aboutToBeYaml, () => {
    tp.app.commands.executeCommandById(
			SORT_FRONTMATTER_CMD_ID
    )
  }).catch((err) => {
    throw new Error(JSON.stringify({err, desc: "gensortyaml error"}))
  })

	const longformFigDivInfo = {
			text: JSON.stringify(longformFig),
			attr: {
				style: "background: green;padding: .5em .5em; border-radius: 5px 5px;",
			}
	}
	const $longformFigDiv = window.createDiv(longformFigDivInfo)

	$frag.$el.replaceChildren($longformFigDiv);
  new obs.Notice(
		$frag.$el,
	  2000
	)
  // ## REFRESH UI
  try {
	  metadataEditor.save()
	  fileView.editor.refresh()
  } catch(err) {
	  log(`${JSON.stringify(err)}: save and refresh error`);
  }

	// #  Utilities;

	function syncFmWithUserData(fm, userData) {
			// if current fm has userData leave alone, if not add to thingie.
			const pkg = { ...fm }
			const insert = {}
			for (let key in userData) {
				const isEmpty = [null,undefined].includes(pkg[key]) || !pkg.hasOwnProperty(key);
				log({isEmpty, key})
				if (isEmpty) {
				// in order to sync, the frontmatter must be pre-told of the change. If the properties don't exist, this won't add to metadata at all.
					insert[key] = userData[key]
				}
			}
			metadataEditor.insertProperties(insert)
			metadataEditor.save()
			return { ...pkg, ...insert };
	}
	function createGenFrontmatterHelper(_timeout = 2000) {
	
		return function genHelper(inyaml, cb, timeout = _timeout) {
			return new Promise((resolve,reject) => {
			
	
				cb()
				setTimeout(() => {
					let ykeys = {}
					const currentYaml = serializeYaml()
					const inyamlLen = Object.keys(inyaml).length
					const currentYamlLen  = Object.keys(
						currentYaml
					).length;
					// never fail
					resolve({isPass: true, pkg: null})
					/**
					if (currentYamlLen <= inyamlLen) {
						resolve({isPass: true, pkg: null})
					} else {
						for ( let k in inyaml) {
							if (!currentYamlLen.hasOwnPropery(k)) {
								ykeys[k] = inyaml[k]
							}
						}
						reject({
							isPass: false,
							pkg: Object.keys(inyaml)
						 })
					}
					**/
				}, timeout)
	
			})
		}
	}
	// the templater version of this code does not have the same ctx.
	async function genCreateFrag(ctx) {
		return new Promise((resolve, rej) => {
			window.createFragment(($el) => {
				ctx.app.workspace.onLayoutReady(() => {
					resolve({$el})
				})
			})
		})
	}
	async function genCreateDiv(ctx, config = {text: '', attr: {}}) {
		const {text, attr} = config;
		const $frag = await genCreateFrag(ctx);
		return new Promise((resolve, reject) => {
			const domInfo = {
				text,
				parent: $frag,
				attr,
			};
			window.createDiv(domInfo, callback)
			function callback($el) {
				ctx.app.workspace.onLayoutReady(() => {
					resolve({$el, $frag})
				})
			}
		})
	}
}
_%>
<%* 
	/**

  const tfile = tp.file.find_tfile(
    tp.file.path(true)
  );

	tp.app.fileManager.processFrontMatter(
		tfile, 
	  async (fm) => {

			setTimeout(() => {
				log({longformFig,fm})
				fm[LONGFORM_FIELD_NAME] = longformFig;
			}, 3000)
			// savedClearID = clearID
			// const rgx = /(?<=v)\d+\.\d+\.\d+/
			// const val = fm[FIELD_NAME]
			// const _val = val.match(rgx).first();
			// const bumped_val = bump(String(_val))
			// fm[FIELD_NAME] = prefix(bumped_val, "v")
			// return;
			// clearID = setTimeout(sortfm, 1000)
	function prefix(str, affix) {
		return affix + str;
	}
	function bump(version, style = "patch") {
		const [major, minor, patch] = version.split('.').map(Number);
		if (style === "patch") {
			return `${major}.${minor}.${patch + 1}`;
		}
		return version;
	}
	function sortfm() {
		const command = this.app.commands
			.findCommand("obsidian-one-ring:sort frontmatter")
		tp.app
			.commands
			.executeCommand(command)
	}
	**/
	
_%>
<%* /** COMMIT LOG
* v0.0.1 *2025-10-16*
	* Last save point that grabs current frontmatter and updates. 
**/_%>
<%* /** Readme 
The goal of this macro is to update the longform.title and the STORY_TITLE in Index files using the frontmatter of the root project folder (MUID and STORY_TITLE)
**/_%>
