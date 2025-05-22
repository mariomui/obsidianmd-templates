> [!info]- 🪭 The following code displays every file's [[,aka-lcsh]]s  as well as any non-classified file. (This [[,aka-codelet]] was written specifically to help [[,aka-index-specced-note]]s deal with lcsh reassignment problems)
> > DEPS: [[≈.~viewfn-for-listing-of-lcsh-headings-from-obsidian-query,nb.-MUID-198,ver.-0.0.2]]

<%-*
tp.app.workspace.onLayoutReady(bootup.bind(this))

function bootup() {

	const utils = {codewrapContent,debug}
	const boundedGenMain = genMain.bind(this);
	try {
		(boundedGenMain)({codewrapContent, debug});
	} catch(err) {console.log(err)}
}

function genMain(utils) {

	tp.hooks.on_all_templates_executed(async () => {
		const choice = await genSuggest()
		const keyword = await genPrompt()
		await genOrchestrateInserts({choice,keyword})
	})
	async function genSuggest() {
		const choices = {YES: true, NO: false}
		const choice_text = "Do you want to add the query as well?"
		const choice = await tp.system.suggester(
				Object.keys(choices), 
				Object.values(choices),
				false, 
				choice_text
		);

		return choice
	}

	async function genPrompt() {
		const default_prompt_value = null;
		const shouldThrowOnCancel = true;
		const keyword = await tp.system.prompt(
			"What keyword do you want queried for scraping?", 
			default_prompt_value, 
			shouldThrowOnCancel
		);
		return keyword
	}
	
	async function genOrchestrateInserts({keyword, choice}) {
		// dynamically source the view partial so that the filename can be changed at will.
		const viewpath = tp.app.metadataCache.getCachedFiles().find((x) => x.contains("nb.-MUID-198"))
		const view_basename = tp.app.vault.getAbstractFileByPath(viewpath)?.basename;
		if (!view_basename) return "broken";
		const viewfn = `![[${view_basename}#=|?search_term=${keyword}&t=nlk]]`
		
		const text = [
			keyword
		].join("");
		
		const wrapped_text = utils.codewrapContent(
			text, "query"
		);
		
		await tp.file.cursor_append("> " + viewfn)
		await tp.file.cursor_append("\n")
		if (choice === false) return;
		
		await tp.file.cursor_append(
			wrapped_text
		);
	}
}
function debug(...args) {
	console.log(...args)
}
function codewrapContent(content, wrapType) {
	const ticks = "\`\`\`";
	return [
		`${ticks}${wrapType}`,
		"\n",
		content,
		"\n",
		ticks,
		"\n"
	].join("")
}
_%>