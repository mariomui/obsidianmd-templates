<%*
// MUID-3118, uses MUID-3117 as base
tp.hooks.on_all_templates_executed(() => {
  const CSS_FIELD = "UMID";
  const CSS_NEW_FIELD = "PROJECT_PARENT"
  const tfile = tp.file.find_tfile(
    tp.file.path(true)
  );
  
	tp.app.fileManager.processFrontMatter(
		tfile, 
	  (fm) => {
			const hasFieldname = fm
				?.hasOwnProperty
				?.call(fm, CSS_FIELD);
				
			if ((fm && !hasFieldname) || !fm) {
				return;
			}
			delete fm[CSS_FIELD]
			Object.assign(
				fm, 
				{ [CSS_NEW_FIELD]: null }
			);
			return;
		}
	)
	setTimeout(sortfm, 1000)
	function sortfm() {
		const command = this.app.commands
			.findCommand("obsidian-one-ring:sort frontmatter")
		tp.app
			.commands
			.executeCommand(command)
	}

})
_%>

