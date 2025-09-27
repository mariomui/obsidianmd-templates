
<%* 
const file_title = tp.file.title
const callout = ` > [!Tip]+ 🪭 About `
const aliased_wikilink = `![[${file_title}#10÷About|10÷Aboutnlk]]`

const content = [callout, `\n`, ` > > `, aliased_wikilink].join("");

tp.app.workspace.onLayoutReady(() => {
tp.file.cursor_append(content)
})
_%>
