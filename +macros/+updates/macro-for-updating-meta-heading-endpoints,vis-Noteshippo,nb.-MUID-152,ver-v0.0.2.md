<%_* /** README 
* date create: *2025-05-03*
* MUID: MUID-152
* Desc: Updates private header child endpoints to latest api paradigm (see knobs); 
	* [[about-header-endpoint,bt.-Noteshippo-heading-api,nb.-common-type]]
	* [[reference-endpoint,bt.-Noteshippo-heading-api,]]
**/_%>
<%_*

// # TOOLS 
const afv = tp.app.workspace.getActiveFileView()
const tfile = tp.file.find_tfile(tp.file.path(true));

// # KNOBS
const ABOUT = "10÷About"
const REFERENCE = "11÷Reference"
const LEVEL = 3;
const [aboutRgx, referenceRgx] = [/About$/, /Reference$/]
const headingFigs = tp.app.metadataCache.getFileCache(tfile).headings;
const privateHeadingFigs = headingFigs.filter((headingFig) => {
	return (headingFig.level === (LEVEL)) && [aboutRgx, referenceRgx].some((rgx) => {
		return headingFig?.heading?.match(rgx);
	})
})

const heading_prefix = "";
const actions = privateHeadingFigs.map(({heading, position}) => {
	let replace_text_with = heading;
	if (heading.match(aboutRgx)) {
		replace_text_with = heading_prefix + " " + ABOUT;
	}
	if (heading.match(referenceRgx)) {
		replace_text_with = heading_prefix + " " + REFERENCE;
	}
	return {heading, position, replace_text_with};
})

const replaceHeadingText = createReplaceHeadingText(
	{afv,tfile}
);
replaceHeadingText(actions)


function createReplaceHeadingText({afv, tfile}) {
	const factoryFig = {
		afv, tfile
	}
	return function _replaceHeadingText(actions, fig = {...factoryFig}) {
		const {afv, tfile} = {...fig, ...factoryFig};
		actions.forEach(({
			heading, position, replace_text_with
		}) => {
			const {start, end} = position;
			afv.editor.replaceRange.call(afv.editor,
				replace_text_with, 
				{ch: start.col + (LEVEL), line: start.line}, 
				{ch: end.col, line: end.line}
			);
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