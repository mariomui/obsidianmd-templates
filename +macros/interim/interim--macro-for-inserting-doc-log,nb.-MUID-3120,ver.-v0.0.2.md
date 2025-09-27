
# ---Transient Doc Log

<%* /** Readme
MUID-3120
**/_%>
<%*

// based off [[,aka-macro-MUID-3118]]

tp.app.workspace.onLayoutReady(bootup.bind(this));

function bootup() {
	try {
		tp.hooks.on_all_templates_executed(mainHook.bind(this));
	} catch(err) {
		console.log({err});
	}

	function mainHook() {
		// KNOBS
		const FIELD_NAME = "DOC_VERSION";
		/**
		const tfile = tp.file.find_tfile(
			tp.file.path(true)
		);
		**/
		const tfile = tp.config.target_file;

		tp.app.fileManager.processFrontMatter(tfile, (fm) => {
			// # Ingredients
			const hasFieldname = fm?.hasOwnProperty?.call(fm, FIELD_NAME);
			const templateFile = tp.config.template_file;

			// scrape macro version.
			const macro_version = templateFile.basename.match(
				/ver\.-\d\.\d\.\d/, "$1"
			)?.first();
			// scrape macro muid
			const muid = templateFile.basename.match(
				/nb\.-MUID-\d+/, "$1"
			)?.first();
			// console.log({macro_version, muid})
			if (!macro_version || !muid) {
				throw new Error("no versioning or id detected in macro filename");
			}

			/**
			const viewpath = tp.app
				.metadataCache.getCachedFiles().find((x) => x.contains(MUID));
			
			const view_basename =
				tp.app.vault.getAbstractFileByPath(viewpath)?.basename;
			**/

			const view_basename = templateFile?.basename;

			if (!view_basename) return "broken";

			const [template, subs] = [
				`@ DOC LOG uti. [[$1]] ($2)`,
				[view_basename, macro_version],
			];

			const display_string = pugit(template, subs);

			if ( (fm && !hasFieldname) || !fm ) {
				tp.file.cursor_append(
					createList(display_string, "v0.0.0")
				);
				return;
			}
// (?<=v) lookahead
			// const rgx = /(?<=v)\d+\.\d+\.\d+/;
			const val = fm[FIELD_NAME];
			tp.file.cursor_append(createList(display_string, val));

			// setTimeout(sortfm, 1000)
			function prefix(str, affix) {
				return affix + str;
			}
			// ui
			function createList(root, nested) {
				let result = `* ${root}`;
				const space = " ";
				result += "\n";
				result += space.repeat(2);
				result += `* ${nested}`;
				return result;
			}
		})
	}
}


/**
 * @param muid {string} ie: "nb.-MUID-000"
 * @param gen...fig {keyword: string, choice: boolean}
 * 
 * @return null 
 * @desc: inserts a dynamically sourced muid, usually a macro this avoids hard coding.
 * @deps: templater, codewrapContent
**/
function pugit(
		template, subs
	) {
	// dynamically source the view partial so that the filename can be changed at will.

	let display_string = template;
	const tokens = template.match(/\$\d+/g);

	for (const [idx, token] of Object.entries(tokens) ) {
		display_string = display_string.replace(token, subs[idx]);
	}

	return display_string;

}

_%>

<%* /**
* Commit Log
* v0.0.2 *2025-05-30*
	* Replaced dataview paradigms of getting target and template file with templater api.
	* Fix muid extractio
* v0.0.1 *2025-05-23*
* v0.0.0 *2025-04-24*
	* Add version number to title.
	* Add DOC LOG root to appended value.
**/ _%>