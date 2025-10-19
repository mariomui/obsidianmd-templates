
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
			let first_line = `## LC--`

			// # DERIVED KNOBS
			const ch = first_line.length || 0;
			
			const cfg = {
				keyword: [].join(""),
			}
			const {
				tFile, wrapped_macro, macro_basename
			} = await genLookupBaseNameUsingMuid("MUID-181",cfg)
			
			const fm = tp?.frontmatter || {}
			const title = fm["title"] ||fm["QUICK_TITLE" || null]
			
			if (title || fm["MUID"]) {
				const quick_title_muid = [title, fm["MUID"]]
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
				editor.setCursor(cursor.line - 3, ch);
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
* MUID: MUID-191
* desc: inserts citum for litnotes
**/_%>
<%_* /**
* v0.0.8* *2025-10-13*
	* Put the entire templating entirely in code so i can grab the QUICK_TITLE and MUID as citation identifiers.
	* Add a title as one of the alternates to quick_title, because its available in the mediadb dbs, autopopped.
* v0.0.7 *2025-05-06*
	* replace this.umid with this.Project_parent
	* Apply [[macro-for-inserting-file-basename,nb.-MUID-181,ver.-v0.0.9]] (v0.0.8)
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
	* change title to use nota bene [[master-list-of-vocabulary,nb.-word,vis-Classical-languages#Nota bene]]
* v0.0.3 2025-01-10*
	* Take out the placeholders as it was getting in the way. i fucking know what i'm doing
* v0.0.2 *2025-01-10*
  * Fixed the problem where the cursor would appear on the first of a literature note. Pasting on top of the note, rather than at the current cursor. Use pure coding instead of templating.
**/
_%>