
<%* /** Readme
This template is working most of the time... dont know why new projects are sometimes not getting templated.
**/_%>
<%*
const title = await tp.file.title;

new tp.obsidian.Notice("Please add an end date. Default is next year.");

this.app.workspace.onLayoutReady(() => {

	// Mutate end date to be 1 year end.
	tp.hooks.on_all_templates_executed(async () => { 
		const tfile = tp.file.find_tfile(
			tp.file.path(true)
		);
		const fv = tp.app.workspace.getActiveFileView()
		const fm = fv.metadataEditor.serialize()
		const futureDate = tp.date.now("YYYY-MM-DD", "P1Y");


		fm["PROJECT_END_DATE"] = futureDate
		await fv.metadataEditor.synchronize(fm);
		await fv.save();
		fv.editor.refresh();
		//refresheditor has been deprecated
	});
})
-%>
