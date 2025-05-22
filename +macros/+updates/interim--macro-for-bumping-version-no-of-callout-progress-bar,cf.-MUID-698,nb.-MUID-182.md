<%_* /** README 
* date create: *2025-05-06*
* MUID: MUID-182	
* Desc: Bumps the version of the internal callout text inside of [[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698]]
**/_%>
<%_*
let BumpStyleOptions;
(function (BumpStyleOptions) {
	BumpStyleOptions["Patch"] = "Patch";
	BumpStyleOptions["Minor"] = "Minor";
})(BumpStyleOptions || (BumpStyleOptions = {}))

// KNOBS
const TARGET_TO_UPDATE = "> [!info]- Progress Bar"
const SECTION_TYPE = "callout"

// # TOOLS 
const afv = tp.app.workspace.getActiveFileView()
const tfile = tp.file.find_tfile(tp.file.path(true));
const replaceText = createReplaceText(
	{afv,tfile}
);
const getLineData = createGetLineData({afv})

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
			TARGET_TO_UPDATE
		}
		
		main.call(this, mainFig);
		
	} catch(err) {
		console.log({err})
	}

}


// workhorse
function main(fig) {
	const {		
		calloutFigs,
		getLineData,
		replaceText,
		sections,
		TARGET_TO_UPDATE
	} = fig;
	const actions = calloutFigs.map(({position}) => {
		const lineData = getLineData(position, TARGET_TO_UPDATE)

		return {lineData};
	})
	replaceText(actions)
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
	* Rename private header to meta heading endpoints
* v0.0.1
	* add MUID, add versioning number
**/_%>