<%*
// based off [[interim--macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-0.0.1]]
// |MUID-145|
const SORT_FRONTMATTER_CMD_ID = "obsidian-one-ring:sort frontmatter";

let FrontmatterFieldnames;
(function (FrontmatterFieldnames) {
	FrontmatterFieldnames["STORY_TITLE"] = "STORY_TITLE";
	FrontmatterFieldnames["LONGFORM"] = "longform";
	FrontmatterFieldnames["MUID"] = "MUID";
})(
	FrontmatterFieldnames || (FrontmatterFieldnames = {})
);
tp.hooks.on_all_templates_executed(async () => {

	const fileView = tp.app.workspace.getActiveFileView()
	
	const metadataEditor = fileView.metadataEditor
	const serializeYaml = metadataEditor.serialize.bind(metadataEditor);
	const synchronizeYaml = metadataEditor.synchronize.bind(metadataEditor);
	await genMain({
      fileView, serializeYaml, metadataEditor, synchronizeYaml, checkHasFieldname
    })
    .catch(console.log)
})


function checkHasFieldname(fig = {}, field_name) {
	return !!fig?.hasOwnProperty?.call(fig, field_name);
}

// workhorse;
async function genMain(pkg) {

	// # factory-created functions that add a little timer to the actions. A stopgap (so I dont actually have to write a task runner)
  const genSynchronizeYaml = createGenFrontmatterHelper(4000)
	const genSortYaml = createGenFrontmatterHelper(2000)

	// # Identfying the dependencies;
  const {
      fileView, serializeYaml, metadataEditor, synchronizeYaml, checkHasFieldname
  } = pkg;

	// # Setting the table
  const fm = serializeYaml();

	// # Early Exit checks
	const isAllFieldnamesExist = Object.values(
		FrontmatterFieldnames
	).every((fn) => {
		const hasFieldname = checkHasFieldname(fm, fn)
		if (!hasFieldname) new tp.obsidian.Notice(
			`${fn} does not exist! Please add! Exiting`,
			2000
		);
		return hasFieldname;
	})
	if (!fm || !isAllFieldnamesExist) {
		throw new Error("not all fields exist");
		return;
	}

	// # Logic

	// ## Update the long form fig.
	const longformFig = fm[FrontmatterFieldnames.LONGFORM]

	// ## temporary update function. 
	const updateLongformField = (field_name, value) => {
		longformFig[field_name] = value;
	}
	const muid_prefixed_story_title = `${fm[FrontmatterFieldnames.MUID]}--${fm[FrontmatterFieldnames.STORY_TITLE]}`;

	updateLongformField(
		"title",
		muid_prefixed_story_title,
	);

	// ## Pre-Sync the fig using metadataEditor. Should also update the metadataCache. 
	const updatedFm = syncFmWithUserData(
    fm,
    {...fm, "longform": longformFig } // custom user data
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
  tp.obsidian.Notice(
	  JSON.stringify(longformFig),
	  2000
	)
  // ## REFRESH UI
  metadataEditor.save()
  fileView.editor.refresh()

	// #  Utilities;

	function syncFmWithUserData(fm, userData) {
			// if current fm has userData leave alone, if not add to thingie.
			const pkg = { ...fm }
			const insert = {}
			for (let key in userData) {
				const isEmpty = [null,undefined].includes(pkg[key]) || !pkg.hasOwnProperty(key);
				console.log({isEmpty, key})
				if (isEmpty) {
				// in order to sync, the frontmatter must be pre-told of the change. 
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
				console.log({longformFig,fm})
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

