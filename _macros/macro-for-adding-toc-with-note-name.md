<%*
const file_title = tp.file.title;
const ADL = `[[≈-for-creating-dictionary-lists-with-transcluded-datum,vis-Dataviewjs#=|ADL-TOC]]`
const TOC = `[[${file_title}#LR--TOC|TOC]]`
const ABOUT = `[[${file_title}#10-About|10-About]]`
tp.file.cursor_append(
	`* ${ABOUT}\n`
)
tp.file.cursor_append(
	`* ${TOC}\n\t* ${ADL}`
);
_%>