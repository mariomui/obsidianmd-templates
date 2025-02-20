<%*
const header = `## LC--citum--`
const reference = "**file_basename**: \`= this.file.name\` \`= this.DOC_VERSION\` `=this.MUID`"
tp.file.cursor_append(`${header}\n`)
tp.file.cursor_append(`\n`)
tp.file.cursor_append(`${reference}\n`)
tp.file.cursor_append(`\n`)
_%>

<%*
/**
* v0.0.4 *2025-02-04*
	* add muid
	* change title to use nota bene [[master-list-of-vocabulary,vis-Classical-languages#Nota bene]]
* v0.0.3 2025-01-10*
	* Take out the placeholders as it was getting in the way. i fucking know what i'm doing
* v0.0.2 *2025-01-10*
  * Fixed the problem where the cursor would appear on the first of a literature note. Pasting on top of the note, rather than at the current cursor. Use pure coding instead of templating.
**/
_%>