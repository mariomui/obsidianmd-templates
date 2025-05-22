
<%* /** Readme
This template is working most of the time... dont know why new projects are sometimes not getting templated.
**/_%>
<%_* 
const title = await tp.file.title;

new tp.obsidian.Notice("Please add an end date. Default is next year.");

// Mutate end date to be 1 year end.
tp.hooks.on_all_templates_executed(async () => { 
	const tfile = tp.file.find_tfile(
		tp.file.path(true)
	);
	const fv = tp.app.workspace.getActiveFileView()
	const fm = fv.metadataEditor.serialize()
	fm["PROJECT_END_DATE"] = tp.date.now("YYYY-MM-DD", 365);
	await fv.metadataEditor.synchronize(fm);
	await fv.save();
	fv.refreshEditor();
});
-%>