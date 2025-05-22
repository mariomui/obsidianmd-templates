<%*
// based off [[interim--macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-0.0.1]]


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

async function genMain(pkg) {
	const LONGFORM_FIELD_NAME = "longform"
	const FIELD_NAME = "draftTitle";
	
  const genSynchronizeYaml = createGenFrontmatterHelper(4000)
	const genSortYaml = createGenFrontmatterHelper(2000)
  const {
      fileView, serializeYaml, metadataEditor, synchronizeYaml, checkHasFieldname
  } = pkg;

  const fm = serializeYaml();

	const hasLongform = checkHasFieldname(fm, LONGFORM_FIELD_NAME);
	if (!fm || !hasLongform) {
		return;
	}
	
	const longformFig = fm[LONGFORM_FIELD_NAME]

	const hasDraftTitle = checkHasFieldname(
		longformFig, FIELD_NAME
	);	
	if ( !hasDraftTitle ) {
		longformFig[FIELD_NAME] = "v0.0.1";
	} else {
		// const draft_title= await tp.system.prompt(
			// "What draftTitle do you want?"
		// );
		const bumped = bump( longformFig[FIELD_NAME] )
		
		longformFig[FIELD_NAME] = bumped;
	}
	
	const updatedFm = syncFmWithUserData(
    fm,
    {...fm, "longform": longformFig } // custom user data
  );
  
  const aboutToBeYaml = { ...updatedFm };

	// # TASKS PIPELINE
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
      "obsidian-one-ring:sort frontmatter"
    )
  }).catch((err) => {
    throw new Error(JSON.stringify({err, desc: "gensortyaml error"}))
  })
  
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
	function bump(val, style = "patch") {
		const rgx = /(?<=v)\d+\.\d+\.\d+/;
		const _val = val.match(rgx)?.first();
		if (!_val) return val;
		
		const bumped_val = bump(String(_val), style)
		return bumped_val;
		
		function bump(version, style) {
			const [major, minor, patch] = version.split('.').map(Number);
			let bumped_version = version;
			if (style === "patch") {
				const patched = `${major}.${minor}.${patch + 1}`;
				bumped_version = prefix(patched, "v");
			}

			return bumped_version;
			
			function prefix(str, affix) {
				return affix + str;
			}
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

