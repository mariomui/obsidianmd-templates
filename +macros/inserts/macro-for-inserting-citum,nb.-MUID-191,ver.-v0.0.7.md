## LC--

**file_bn--v0.0.7**: *`= this.file.name`* doc-`=this.DOC_VERSION` `= this.MUID`/`=this.heading`/`=this.PROJECT_PARENT`/

<%* /** README
* MUID: MUID-191
* desc: inserts citum for litnotes
**/_%>
<%_* /**
* v0.0.7 *2025-05-06*
	* replace this.umid with this.Project_parent
* v0.0.6 *2025-03-11*
	* remove § :opt: + 6 because i cant remember opt 6 and i dont wnat to fix the lc citums in the zotero templates.
	* prefix § to LC to further differentiate it when I call for it via bracket search
* v0.0.5 *2025-03-10*
	* Remove citum 
		* LC--t10m33-- format still applies.
	* Return to non coded version. The fix in 0.0.2 is because of css and plugin lag brought about by bad plugins
	* Update to v0.0.4 of file basename
	* archive code
		* const header = `## LC--citum--`
		* const reference = "**file_basename**: \`= this.file.name\` \`= this.DOC_VERSION\` `=this.MUID`"
		* tp.file.cursor_append(`${header}\n`)
		* tp.file.cursor_append(`\n`)
		* tp.file.cursor_append(`${reference}\n`)
		* tp.file.cursor_append(`\n`)
* v0.0.4 *2025-02-04*
	* add muid
	* change title to use nota bene [[master-list-of-vocabulary,vis-Classical-languages#Nota bene]]
* v0.0.3 2025-01-10*
	* Take out the placeholders as it was getting in the way. i fucking know what i'm doing
* v0.0.2 *2025-01-10*
  * Fixed the problem where the cursor would appear on the first of a literature note. Pasting on top of the note, rather than at the current cursor. Use pure coding instead of templating.
**/
_%>