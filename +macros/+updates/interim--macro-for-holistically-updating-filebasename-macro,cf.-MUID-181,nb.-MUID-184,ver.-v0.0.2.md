<%_* /** README 
* date create: *2025-05-06*
* MUID: MUID-184
* Desc: Bumps the filename semver AND the content semver of [[macro-for-inserting-file-basename,nb.-MUID-181,ver.-v0.0.7]]
* Definition:
	* single purpose means it only updates MUID-181
		* The opposite would be genpop-purpose
	* holistic means it updates the file contents (filebn v0.0.4) AND the filename
**/_%>
<%_*
// const { default: obs } = this.app.plugins.plugins["templater-obsidian"].templater.current_functions_object.obsidian;

let BumpStyleOptions;
(function (BumpStyleOptions) {
	BumpStyleOptions["Patch"] = "Patch";
	BumpStyleOptions["Minor"] = "Minor";
})(BumpStyleOptions || (BumpStyleOptions = {}))

// KNOBS
const TARGET_TO_UPDATE = "`= this.file.name`* doc-`=this.DOC_VERSION` `= this.MUID`/`=this.heading`/`=this.PROJECT_PARENT`/";
const SECTION_TYPE = "paragraph"

// # TOOLS 
const afv = tp.app.workspace.getActiveFileView()
const tfile = tp.file.find_tfile(tp.file.path(true));

// ## factory functions
const replaceText = createReplaceText(
	{afv,tfile}
);
const getLineData = createGetLineData({afv})
const genRenameFile = createGenRenameFile({tfile});

tp.app.workspace.onLayoutReady(bootstrap.bind(this));

function bootstrap() {
	// # KNOBS


	// # LOGIC
	try {
		const { sections } = tp.app.metadataCache.getFileCache(tfile);
		const calloutFigs = sections.filter((section) => {
			return section.type === SECTION_TYPE
		})
		const mainFig = {
			calloutFigs,
			getLineData,
			replaceText,
			sections,
			TARGET_TO_UPDATE,
			genOverridePluginSetting
		}
		const boundedGenMain = genMain.bind(this); // why can't i bind genMain by calling it?
 	(boundedGenMain)(mainFig); 
		
	} catch(err) {
		console.log({err})
	}

}


 // workhorse 
async function genMain(fig) {
	const {		
		calloutFigs,
		getLineData,
		replaceText,
		sections,
		TARGET_TO_UPDATE,
		genOverridePluginSetting
	} = fig;
	const actions = calloutFigs.map(({position}) => {
		const lineData = getLineData(position, TARGET_TO_UPDATE)
		return {lineData};
	})
	replaceText(actions)
	await genRenameFile(); 
}

function createGenRenameFile({tfile}) {
	const title = tfile.name
	
	return async function _genRenameFile(style = BumpStyleOptions.Patch) {
		const ver = extractVerFromText(title);
		if (!ver) throw new Error("no ver in createrenamefile")
		const bumped_ver = bump(ver,style)
		const new_title = title?.replace(ver, bumped_ver)  
		const join = this.app.vault.adapter.path.join
		const new_path = join(tfile.parent.path, new_title);
		// console.log(tp.obsidian.normalizePath(new_path));

		await genOverridePluginSetting("auto-note_mover", "trigger_auto_manual", "Manual");
		// 🐛 https://forum.obsidian.md/t/duplication-files-with-method-filemanager-renamefile-file-newpath/83966/8
		
		await this.app.fileManager.renameFile(tfile, new_path)
		
		await genOverridePluginSetting("auto-note_mover", "trigger_auto_manual", "Automatic");
	}
}

async function genOverridePluginSetting(pluginName, prop, state) {
	const prevState = this.app.plugins.plugins["auto-note-mover"].settings[prop];
	
	this.app.plugins.plugins["auto-note-mover"].settings[prop] = state;
	
	await this.app.plugins.plugins["auto-note-mover"].loadSettings();
}
function extractVerFromText(val) {
	const rgx = /(?<=v)\d+\.\d+\.\d+/
	const _val = val.match(rgx)?.first();
	return _val;
}
function bump(version, style = BumpStyleOptions.Patch) {
	const [major, minor, patch] = version.split('.').map(Number);
	if (style === BumpStyleOptions.Patch) {
		return `${major}.${minor}.${patch + 1}`;
	}
	return version;
}
function createGetLineData({afv}) {
	const curryFig = {
		afv
	}
	return function _getLineData(position, target_text) {
		const {start, end} = position;
		for (let i = start.line; i <= end.line; i++) {
			const line_content = afv.editor.getLine(i);
			if (line_content.contains(target_text)) {
			// console.log({line_content, target_text}, "contains")
				return {line_no: i, line_content};
			}
		}

		return null;
	}
}
function createReplaceText({afv, tfile}) {
	const curryFig = {
		afv, tfile
	}
	return function _replaceText(actions, fig = {...curryFig}) {
		const {afv, tfile} = {...fig, ...curryFig};
		actions.forEach(({
			lineData
		}) => {
			const {line_content, line_no} = lineData;
			const ver = extractVerFromText(line_content);

			const bumped_ver = bump(ver);
			const replaced = line_content.replace(ver, bumped_ver);
			afv.editor.replaceRange.call(afv.editor, replaced, {ch: 0, line: line_no}, {ch: line_content.length, line: line_no})
		})
	}
}
// afv.editor.replaceRange("## 10-Boo", {ch: 0, line: 27}, {ch: 12, line: 27})
_%>
<%_* /**
* v0.0.2 *2025-05-06*
	* Also rename the file to the new updated bumped version. It is necessary to disable and then renable automover during this process.
	* Rename private header to meta heading endpoints
* v0.0.1
	* add MUID, add versioning number
**/_%>