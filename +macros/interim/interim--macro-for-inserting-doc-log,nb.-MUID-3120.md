
# ---Transient Doc Log

- 🔗 [[interim--macro-for-inserting-doc-log,nb.-MUID-3120]]
<%*
// KNOBS
const MACRO_VERSION = "v0.0.1"
const MUID = "MUID-3120"

// based off [[interim--macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-0.0.1]]
tp.hooks.on_all_templates_executed(() => {
  const FIELD_NAME = "DOC_VERSION";
  const tfile = tp.file.find_tfile(
    tp.file.path(true)
  );
  
	tp.app.fileManager.processFrontMatter(
		tfile, 
	  (fm) => {
			const hasFieldname = fm
				?.hasOwnProperty
				?.call(fm, FIELD_NAME);

			const ROOT_LABEL = `@ DOC LOG uti. [[,aka-macro-${MUID}]] ${MACRO_VERSION}`
			if ((fm && !hasFieldname) || !fm) {
				tp.file.cursor_append(
					createList(ROOT_LABEL, "v0.0.0")
				);
				return;
			}
			const rgx = /(?<=v)\d+\.\d+\.\d+/
			const val = fm[FIELD_NAME]
			tp.file.cursor_append(
				createList(ROOT_LABEL, val)
			);

			return;
		}
	)
	setTimeout(sortfm, 1000)
	function prefix(str, affix) {
		return affix + str;
	}
	// ui
	function createList(root, nested) {
		let result = `* ${root}`
		const space = " ";
		result += "\n";
		result += space.repeat(2);
		result += `* ${nested}`;
		return result;
	}
});
_%>

<%* /**
* Commit Log
* v0.0.0 *2025-04-24*
	* Add version number to title.
	* Add DOC LOG root to appended value.
**/ _%>
