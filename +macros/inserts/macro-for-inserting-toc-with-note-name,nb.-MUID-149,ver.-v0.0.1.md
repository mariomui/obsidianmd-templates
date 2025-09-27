
<%*
const file_title = tp.file.title;

// dependencies;
const ADL = `[[~view-for-creating-dictionary-lists-with-transcluded-datum,vis-Dataviewjs,nb.-MUID-1022#=|ADL-TOC]]`
const TOC = `[[${file_title}#LR--TOC|TOC]]`
const ABOUT = `[[${file_title}#10÷About|10÷About]]`

tp.file.cursor_append(
	`* ${ABOUT}\n`
)
tp.file.cursor_append(
	`* ${TOC}\n\t* ${ADL}`
);
_%>
<%* 
/** Readme
* # Dependencies
	* ## About endpoint
		* Any changes to the About api endpoint does not propagate. This is a larger issue shared by templates. Be careful of dependency changes to the the [[about-header-endpoint,bt.-Noteshippo-heading-api,]]
	* ## 💀 note-title dependency: 
		* [[~view-for-creating-dictionary-lists-with-transcluded-datum,vis-Dataviewjs,nb.-MUID-1022]](for the automatic dictionary list)
			* 💁 [[automatically-update-internal-links,bt.-Obsidianmd-app-feature]]
				* 🔑 As of *2025-05-01* Obsidian's [[,aka-AUIL-feature]] updates inside fenced [[code-block,vis-Obsidianmd-app,]]s 💀 Macro breaks when the 1022 dependency changes in any way because Obsidianmd's automatically update internal links (AUIL) feature does not function within templater
	* 
**/ _%>
<%* /** Commit Log
* v0.0.2
	* Update readme
* v0.0.1
	* tie this macro to muid-1022 because the link to muid-1022 is hardcoded. 
**/ _%>