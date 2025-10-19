
<%_*

	// # TOOLS
	const { MarkdownView } = tp.obsidian;
	const { metadataCache } = tp.app;
	const utils = {codewrapContent}

	tp.app.workspace.onLayoutReady(() => {
		tp.hooks.on_all_templates_executed(genTpBootstrap)
	})
	
	async function genTpBootstrap() {
			// # KNOBS 
			let first_line = `## LC--÷`
			const cfg = {
				keyword: [].join(""),
			}
			const {
				tFile, wrapped_macro, macro_basename
			} = await genLookupBaseNameUsingMuid("MUID-181",cfg)
			
			const fm = tp?.frontmatter || {}
			
			if (fm["QUICK_TITLE"] || fm["MUID"]) {
				const quick_title_muid = [fm["QUICK_TITLE"],fm["MUID"]]
					.filter(Boolean).join(",cf. ");
				first_line = `${first_line},cf. ${quick_title_muid}`
			}

			const evaluated_macro = await tp.file.include(wrapped_macro)

			await tp.file.cursor_append(first_line);
			await tp.file.cursor_append("\n\n" + evaluated_macro);
			const view = tp.app.workspace.getActiveViewOfType(MarkdownView);
			if (view) {
				const cursor = view.editor.getCursor();
				const editor = view.editor
				// manually set it cuz lazy
				editor.setCursor(cursor.line - 3, 7);
			}
	}
	// 🔗 Inspired by [[list-of-codelets,by-x,uti.-templater-plugin,vis-Obsidianmd-app#÷Insert Dynamic Internal Links With Macros]]
	async function genLookupBaseNameUsingMuid(muid, {keyword, codewrapContent}) {
		// dynamically source the view partial so that the filename can be changed at will.
		const view_path = tp.app.metadataCache.getCachedFiles()
			.find(
				(x) => x.contains("nb.-" + muid)
			);
		const tFile = tp.app.vault.getAbstractFileByPath(
			view_path
		);
		
		const macro_basename = tFile?.basename;
		const macro_filename = tFile?.name;
		// err escape. 
		
		if (!macro_basename) throw new Error("file does not exist");

		// Purposefully violating SRP.
		const wrapped_macro = utils.codewrapContent(
			macro_basename + keyword, "brackets"
		);
		
		return {tFile, macro_basename, macro_filename, wrapped_macro}
	}

	// # Utils 
	function codewrapContent(content, wrap_type) {
		const ticks = "\`\`\`";
		if (wrap_type === "query") {
			return [
				`${ticks}${wrapType}`,
				"\n",
				content,
				"\n",
				ticks,
				"\n"
			].join("")
		}
		if (wrap_type === "brackets" ) {
			return [
				`[[`,
				content,
				`]]`
			].join("")
		}
	}
	function getFrontMatterFromFilePath(file_path, cfg = { metadataCache }) {
	  const vf = getVeeFileByRelativePath(file_path);
	  return cfg.metadataCache.getFileCache(vf)?.frontmatter || {}
	}
	
	function getVeeFileByRelativePath(
	  file_path,
	  relative_path = "",
	  cfg = { metadataCache }
	) {
	  const result = cfg.metadataCache.getFirstLinkpathDest(
	    file_path, relative_path
	  );
	  
	  return result?.[0] || result;
	}
_%>
<%* /** README
* MUID: MUID-227
* desc: inserts citum that are specifically designed to be used in the litnote but not meant for general consumption
	* ! Although nothing is theoretically stopping anyone from consuming them.
**/*%>
<%** /**
* v0.0.2
	* Make cursor go to the correct place after insert.
* v0.0.1
	* [[interim--locked-endpoint-symbol,uti.-÷,bt.-Noteshippo-heading-level-affix,]]
**/
_%>
