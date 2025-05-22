<%_*
// based off [[interim--macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-0.0.1]]
let BumpStyleOptions;
(function (BumpStyleOptions) {
	BumpStyleOptions["Patch"] = "Patch";
	BumpStyleOptions["Minor"] = "Minor";
})(BumpStyleOptions || (BumpStyleOptions = {}))
tp.hooks.on_all_templates_executed(() => {
  const FIELD_NAME = "DOC_VERSION";
  const BUMP_OPTION_FN = "BUMP_OPTION"
  const tfile = tp.file.find_tfile(
    tp.file.path(true)
  );
  
	tp.app.fileManager.processFrontMatter(
		tfile, 
	  (fm) => {
			const hasFieldname = fm
				?.hasOwnProperty
				?.call(fm, FIELD_NAME);
				
			if ((fm && !hasFieldname) || !fm) {
				fm[FIELD_NAME] = "v0.0.1";
				return;
			}
		  const bump_style = fm?.[BUMP_OPTION_FN] || BumpStyleOptions.Patch
		  
			const rgx = /(?<=v)\d+\.\d+\.\d+/
			const val = fm[FIELD_NAME]
			const _val = val.match(rgx)?.first();
			if (!_val) {
				new tp.obsidian.Notice("non semver value in " + FIELD_NAME + " field")
				return;
			}
			const bumped_val = bump(
				String(_val),
				bump_style
			)
			fm[FIELD_NAME] = prefix(bumped_val, "v")
			console.log({fm})
			return;
		}
	)
	setTimeout(sortfm, 1000)
	function prefix(str, affix) {
		return affix + str;
	}
	function bump(version, style = BumpStyleOptions.Patch) {
		const [major, minor, patch] = version.split('.').map(Number);
		if (style === BumpStyleOptions.Patch) {
			return `${major}.${minor}.${patch + 1}`;
		}
		return version;
	}
	function sortfm() {
		const command = this.app.commands
			.findCommand("obsidian-one-ring:sort frontmatter")
		tp.app
			.commands
			.executeCommand(command)
	}
})
_%>

