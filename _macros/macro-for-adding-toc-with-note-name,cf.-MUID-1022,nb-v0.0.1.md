
<%*
const file_title = tp.file.title;
const ADL = `[[~view-for-creating-dictionary-lists-with-transcluded-datum,vis-Dataviewjs,nb.-MUID-1022#=|ADL-TOC]]`
const TOC = `[[${file_title}#LR--TOC|TOC]]`
const ABOUT = `[[${file_title}#10-About|10-About]]`
tp.file.cursor_append(
	`* ${ABOUT}\n`
)
tp.file.cursor_append(
	`* ${TOC}\n\t* ${ADL}`
);
_%>

<%* /**
* v0.0.1
	* tie this macro to muid-1022 because the link to muid-1022 is hardcoded. Macro breaks when this 1022 dependency changes in any way. No auto propagation, unf.
**/ _%>