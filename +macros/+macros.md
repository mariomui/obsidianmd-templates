---
aliases:
  - __README__Y_templates/+macros
  - Y_templates/+macros
tags:
  - _meta
---

# -

* [x] 🔑 I do not use [[aidenlx-folder-note-plugin,bt.-Obsidianmd-app,]] anymore. 💀Create a similar syncing note for this folder page template so that the aidenx folder note stuff can sync correctly to a folder template like note refactor does #_todo/97-unwilling--/to-code ➕ 2023-11-15 ✅ 2025-09-29

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`



# =

**base_filepath-v0.0.9**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT`,alias: *`= this.aliases`*,nb: *`=this.NOTA_BENE`* , authors: *`= this.authors`* / lcsh: `= link(this.heading)`

- ! The stub links are great safeguards for bad sync situations. They keep a record of the previous note title so you can propagate changes, should the first propagation crashed.

- @ Content updaters
	* [[macro-for-updating-meta-heading-endpoints,vis-Noteshippo,nb.-MUID-152,ver-v0.0.2]]
* @ Metadata Level
	* # Versioning
		* [[interim--macro-for-bumping-doc-version-frontmatter-property-value,nb.-semver-patch,nb.-MUID-141]]
		* [[interim--macro-for-bumping-template-version-frontmatter-property-value,nb.-semver-patch,nb.-MUID-153,ver.-v0.0.1]]
	* [[interim--macro-to-toggle-colorgrammar-in-cssclasses-yaml-field,nb.-MUID-3117]]
	* [[macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-v0.0.1]]
	* # Longform
		* [[interim--macro-for-updating-longform-title-with-project-title,nb.-MUID-145,nb.-ver.-v0.0.1,ad-hoc-Longform-Index]]
		* [[macro-for-prompted-update-of-longform-draft-title,nb.-MUID-140,ad-hoc-Longform-Index]]
* @ Content Inserters
	* [[macro-for-automatic-toc,nb.-MUID-148,cf.-MUID-146,ver.-v0.0.4]]
	* # Tasks
		* [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]]
	* [[interim--macro-for-inserting-doc-log,nb.-MUID-3120,ver.-v0.0.2]]
	* [[macro-for-inserting-noteshippo-private-header-api-endpoint,nb.-MUID-151,ver.-v0.0.3]]
* [[,aka-macro-MUID-3123]]
- ! Use the following to determine the types of folders to create
* ! 🛏 TODO
	* 💀 [[∑.≠.ø--macro-for-eec-tline]]
	* [[ø--macro-for-commonly-used-file-and-filepaths-inserts]]
	* [[ø--macro-for-inserting-file-basename-into-litnote]]
	* [[ø--macro-for-sluicing-waypoint-links-into-jobs]]
* # Codelet Notes, used for
	* [[macro-for-inserting-comment-outs,uti.-templater-plugin,vis-Obsidianmd-app,nb.-MUID-180,ver.-v0.0.2]]
	* [[macro-for-insert-of-all-inlink-endpoint,uti.-inline-dql,cf.-MUID-128,nb.-MUID-150,ver.-v0.0.5]]
* @ Note spec
  * [[∑.macro-for-inserting-library-entry-bullet-guide,vis-Writeshippo]]
  * # LCSH
    * [[macro-for-prompted-lcsh-specced-note-template,nb.-MUID-142]]
  * # Library Notes, used for
    * [[macro-for-vocabulary-details,uti.-emoji]]
  * # Source notes, used for
    * [[macro-for-inserting-citum,nb.-MUID-191,ver.-v0.0.8]]
    * ## Media notes
      * [[∑--macro-yaml-update-of-tv-series-frontmatter,nb.-MUID-3136]]
        *  [[media-db-plugin,bt.-ObsidianMD-app,]]
* @ Fiction helpers
	* [[+longform]]
* @ General Note-api Endpoints/Metadata, inserting
	* [[interim--macro-inserting-private-lc-citum]]
	* [[macro-for-inserting-toc-with-note-name,nb.-MUID-149,ver.-v0.0.1]]
	* [[macro-for-insert-of-all-inlink-endpoint,uti.-inline-dql,cf.-MUID-128,nb.-MUID-150,ver.-v0.0.5]]
	* [[macro-for-inserting-base-filepath,nb.-MUID-161,ver.-v0.0.9]]
	* [[interim--macro-for-inserting-abstract-emoji-tocs]]
* @ Tables
	* [[macro-for-inserting-iherdc-template,vis-Characterization,nb.-MUID-230,ver.-v0.0.1]]
- @ Bullet Guides
	* [[interim--macro-for-keyboard-shortcut-bullet-guide,nb.-MUID-203,ver.-v0.0.1]]
	* [[macro-for-inserting-file-basename,nb.-MUID-181,ver.-v0.0.9]]
	* [[interim--macro-for-inserting-organizing-resource-subdivisions,nb.-MUID-226,ver.-v0.0.2,nb.-WBS,nb.-CLKRL,vis-Writing]]
* @ Strategy
  * [[∑--macro-for-stratagem-details]]
* @ Scraping
	* [[macro-for-lcsh-heading-field-query-and-scrape-v1.0.2,uti.-MUID-1934]]
	* [[~viewfn-for-sluicing-out-embedded-query-into-a-job-queue,nb.-MUID-1934A]]
	* [[macro-for-sluicing-out-waypoints]]
	* [[macro-for-targetting-Subject-seeds]]
	* [[macro-for-targetting-unfinished-note-seeds,nb.-MUID-215]]
* @ Query makers
	* ! Make indicator of macro dynamism
		* [[interim--macro-inserting-query-for-targetted-text-in-h2-links]]

* [[interim--macro-for-bumping-version-no-of-callout-progress-bar,cf.-MUID-698,nb.-MUID-182]]
* [[macro-for-bumping-content-and-title-semver-of-macro-MUID-181,nb.-MUID-184,ver.-v0.0.2]]
* [[macro-for-inserting-base-filepath,nb.-MUID-161,ver.-v0.0.9]]
* [[∑--macro-insert-inlink-heading-api,nb.-titled-with-macro,ver.-v0.0.1]]
* [[≈.interim--macro-for-choice-prompted-kanban-root-label-insertion,nb.-MUID-197,ver.-v0.0.1]]
* [[interim--macro-for-displaying-metadata-rating-of-mediadb-notes]]
* [[interim--macro-for-grammatical-classification-affix,ad-hoc-vocabulary-term,nb.-MUID-213,ver.-v0.0.1]]
* [[interim--macro-for-targetting-callout-questions,nb.-MUID-220]]
* [[interim--macro-for-targetting-workflow-affixed-top-level-item,uti.-folding-callout,nb.-MUID-190]]
* [[interim--macro-sluicing-unique-lcsh-headings-and-unclassified-notes,ad-hoc.-proper-lcsh-assignment,nb.-MUID-202,cf.-MUID-198,ver.-v0.0.1]]
* [[macro-for-prompted-scraping-for-specific-filename-using-embedded-query,ver.-v0.0.2,uti.-MUID-1934A]]
* [[∑--macro-for-novel-plotting-template,uti.-outline,vis-Writeshippo,nb.-MUID-223]]
* [[∑--macro-for-targetting-Noteshippo-about-endpoint,nb.-hard-deps,nb.-MUID-221]]
* [[≈-testing-multiple-async-fires-executing-sequentially-within-on_all_templates_executed,nb.-templater-plugin]]
* [[macro-for-scraping-transient-local-citations-and-resources,nb.-MUID-3123,cf.-MUID-1560,ver.-v0.0.3]]

# ---Transient

# ---Transient Jobs

![[~viewfn-sluicing-out-waypoint-like-unprocessed-links,nb.-MUID-1643#=|?search_term=---Transient Waypoints&t=nlkno-uiscroll]]

# ---Transient Waypoints

%% Begin Waypoint %%
- [[∑--macro-for-stratagem-details]]
- [[∑.macro-for-inserting-library-entry-bullet-guide,vis-Writeshippo]]
- **[[+longform]]**
- **+updates**
	- [[interim--macro-for-bumping-version-no-of-callout-progress-bar,cf.-MUID-698,nb.-MUID-182]]
	- [[macro-for-bumping-content-and-title-semver-of-macro-MUID-181,nb.-MUID-184,ver.-v0.0.2]]
	- [[macro-for-updating-meta-heading-endpoints,vis-Noteshippo,nb.-MUID-152,ver-v0.0.2]]
- **inserts**
	- [[macro-for-automatic-toc,nb.-MUID-148,cf.-MUID-146,ver.-v0.0.4]]
	- [[macro-for-insert-of-all-inlink-endpoint,uti.-inline-dql,cf.-MUID-128,nb.-MUID-150,ver.-v0.0.5]]
	- [[macro-for-inserting-base-filepath,nb.-MUID-161,ver.-v0.0.9]]
	- [[macro-for-inserting-citum,nb.-MUID-191,ver.-v0.0.8]]
	- [[macro-for-inserting-file-basename,nb.-MUID-181,ver.-v0.0.9]]
	- [[macro-for-inserting-iherdc-template,vis-Characterization,nb.-MUID-230,ver.-v0.0.1]]
	- [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]]
	- [[macro-for-inserting-locked-endpoint-citums,nb.-MUID-227,ver.-v0.0.2]]
	- [[macro-for-inserting-toc-with-note-name,nb.-MUID-149,ver.-v0.0.1]]
- **interim**
	- [[∑--macro-insert-inlink-heading-api,nb.-titled-with-macro,ver.-v0.0.1]]
	- [[≈.interim--macro-for-choice-prompted-kanban-root-label-insertion,nb.-MUID-197,ver.-v0.0.1]]
	- [[interim--macro-for-bumping-doc-version-frontmatter-property-value,nb.-semver-patch,nb.-MUID-141]]
	- [[interim--macro-for-bumping-template-version-frontmatter-property-value,nb.-semver-patch,nb.-MUID-153,ver.-v0.0.1]]
	- [[interim--macro-for-displaying-metadata-rating-of-mediadb-notes]]
	- [[interim--macro-for-grammatical-classification-affix,ad-hoc-vocabulary-term,nb.-MUID-213,ver.-v0.0.1]]
	- [[interim--macro-for-inserting-abstract-emoji-tocs]]
	- [[interim--macro-for-inserting-doc-log,nb.-MUID-3120,ver.-v0.0.2]]
	- [[interim--macro-for-inserting-organizing-resource-subdivisions,nb.-MUID-226,ver.-v0.0.2,nb.-WBS,nb.-CLKRL,vis-Writing]]
	- [[interim--macro-for-keyboard-shortcut-bullet-guide,nb.-MUID-203,ver.-v0.0.1]]
	- [[interim--macro-for-targetting-callout-questions,nb.-MUID-220]]
	- [[interim--macro-for-targetting-workflow-affixed-top-level-item,uti.-folding-callout,nb.-MUID-190]]
	- [[interim--macro-for-updating-longform-title-with-project-title,nb.-MUID-145,nb.-ver.-v0.0.1,ad-hoc-Longform-Index]]
	- [[interim--macro-inserting-private-lc-citum]]
	- [[interim--macro-inserting-query-for-targetted-text-in-h2-links]]
	- [[interim--macro-sluicing-unique-lcsh-headings-and-unclassified-notes,ad-hoc.-proper-lcsh-assignment,nb.-MUID-202,cf.-MUID-198,ver.-v0.0.1]]
	- [[interim--macro-to-toggle-colorgrammar-in-cssclasses-yaml-field,nb.-MUID-3117]]
	- [[macro-for-inserting-noteshippo-private-header-api-endpoint,nb.-MUID-151,ver.-v0.0.3]]
- [[macro-for-inserting-comment-outs,uti.-templater-plugin,vis-Obsidianmd-app,nb.-MUID-180,ver.-v0.0.2]]
- [[macro-for-lcsh-heading-field-query-and-scrape-v1.0.2,uti.-MUID-1934]]
- [[macro-for-prompted-lcsh-specced-note-template,nb.-MUID-142]]
- [[macro-for-prompted-scraping-for-specific-filename-using-embedded-query,ver.-v0.0.2,uti.-MUID-1934A]]
- [[macro-for-scraping-transient-local-citations-and-resources,nb.-MUID-3123,cf.-MUID-1560,ver.-v0.0.3]]
- [[macro-for-sluicing-out-waypoints]]
- [[macro-for-targetting-finished-note-seeds,nb.-MUID-229]]
- [[macro-for-targetting-Subject-seeds]]
- [[macro-for-targetting-unfinished-note-seeds,nb.-MUID-215]]
- [[macro-for-vocabulary-details,uti.-emoji]]
- [[macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-v0.0.1]]
- **wips**
	- [[∑--macro-for-novel-plotting-template,uti.-outline,vis-Writeshippo,nb.-MUID-223]]
	- [[∑--macro-for-targetting-Noteshippo-about-endpoint,nb.-hard-deps,nb.-MUID-221]]
	- [[∑--macro-yaml-update-of-tv-series-frontmatter,nb.-MUID-3136]]
	- [[∑.≠.ø--macro-for-eec-tline]]
	- [[≈-testing-multiple-async-fires-executing-sequentially-within-on_all_templates_executed,nb.-templater-plugin]]

%% End Waypoint %%
