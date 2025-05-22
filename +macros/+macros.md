---
aliases:
  - __README__Y_templates/+macros
  - Y_templates/+macros
tags:
  - _meta
---

# -

* [ ] Create a similar syncing note for this folder page template so that the aidenx folder note stuff can sync correctly to a folder template like note refactor does ➕ 2023-11-15

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`



# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`


* [[macro-for-updating-meta-heading-endpoints,vis-Noteshippo,nb.-MUID-152,ver-v0.0.2]]
* [[macro-for-inserting-automatic-toc,nb.-MUID-148,cf.-MUID-146,ver.-v0.0.3]]
* [[interim--macro-for-bumping-doc-version-frontmatter-property-value,nb.-semver-patch,nb.-MUID-141]]
* [[interim--macro-for-bumping-template-version-frontmatter-property-value,nb.-semver-patch,nb.-MUID-153]]
* [[interim--macro-for-inserting-doc-log,nb.-MUID-3120]]
* [[interim--macro-for-updating-longform-title-using-muid-and-STORY_TITLE,nb.-MUID-145]]
* [[interim--macro-to-toggle-colorgrammar-in-cssclasses-yaml-field,nb.-MUID-3117]]
* [[interim--macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-0.0.1]]
* [[macro-for-inserting-noteshippo-private-header-api-endpoint,nb.-MUID-151,ver.-v0.0.2]]
* [[macro-for-prompted-update-of-longform-drafttitle,nb.-MUID-140]]
* [[macro-for-scraping-transient-local-citations-and-resources,nb.-MUID-3123]]
- ! Use the following to determine the types of folders to create
* # Tasks
	* [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]]
* ! 🛏 TODO
	* 💀 [[∑.≠.ø--macro-for-eec-tline]]
	* [[ø--macro-for-commonly-used-file-and-filepaths-inserts]]
	* [[ø--macro-for-inserting-file-basename-into-litnote]]
	* [[ø--macro-for-sluicing-waypoint-links-into-jobs]]
* # Codelet Notes, used for
	* [[macro-for-inserting-comment-outs,uti.-templater-plugin,vis-Obsidianmd-app,nb.-MUID-180,ver.-v0.0.2]]
	* [[∑--macro-insert-inlink-heading-api,nb.-titled-with-macro,nb.-v0.0.1]]
* @ Note spec
  * [[∑.macro-for-inserting-library-entry-bullet-guide,vis-Writeshippo]]
  * # LCSH
    * [[macro-for-prompted-lcsh-specced-note-template,nb.-MUID-142,nb.-v0.0.10]]
  * # Library Notes, used for
    * [[macro-for-vocabulary-details,by-emoji]]
  * # Source notes, used for
    * [[macro-for-inserting-citum,nb.-MUID-191,ver.-v0.0.7]]
    * ## Media notes
      * [[∑--macro-yaml-update-of-tv-series-frontmatter,nb.-MUID-3136]]
        *  [[media-db-plugin,bt.-ObsidianMD-app,]]
* @ Fiction helpers
	* [[+longform]]
* @ General Note-api Endpoints/Metadata, inserting
	* [[interim--macro-inserting-private-lc-citum]]
	* [[macro-for-inserting-toc-with-note-name,nb.-MUID-149,ver-v0.0.1]]
	* [[macro-for-insert-of-all-inlink-endpoint,uti.-inline-dql,cf.-MUID-128,nb.-MUID-150,ver.-0.0.5]]
	* [[macro-for-inserting-base-filepath,nb.-MUID-161,ver.-v0.0.6]]
	* [[interim--macro-for-inserting-abstract-emoji-tocs]]
* @ Tables
	* [[macro-for-inserting-iherdc-template,vis-Characterization]]
- @ Bullet Guides
	* [[interim--macro-inserting-keyboard-shortcut-bullet-guide]]
	* [[macro-for-rating-books]]
	* [[macro-for-inserting-file-basename,nb.-MUID-181,ver.-v0.0.7]]
	* [[interim--macro-for-inserting-organizing-resource-subdivisions,ver.-v0.0.1,vis-Writing]]
* @ Strategy
  * [[macro-for-stratagem-details]]
* @ Scraping
	* [[macro-for-lcsh-heading-field-query-and-scrape-v1.0.2,uti.-MUID-1934]]
	* [[macro-for-prompted-scraping-for-specific-filename-using-embedded-query,nb.-v0.0.2,uti.-MUID-1934A]]
	* [[macro-for-sluicing-out-waypoints]]
	* [[macro-for-targetting-Subject-seeds]]
	* [[macro-for-targetting-note-seeds]]
* @ Query makers
	* ! Make indicator of macro dynamism
		* [[interim--macro-inserting-query-for-targetted-text-in-h2-links]]

# ---Transient 010 Jobs

![[~viewfn-sluicing-out-waypoint-like-unprocessed-links,nb.-MUID-1643#=|?search_term=---Transient Waypoints&t=nlkno-uiscroll]]

# ---Transient Waypoints

%% Begin Waypoint %%
- [[∑.macro-for-inserting-library-entry-bullet-guide,vis-Writeshippo]]
- **[[+longform]]**
- **+updates**
	- [[interim--macro-for-bumping-version-no-of-callout-progress-bar,cf.-MUID-698,nb.-MUID-182]]
	- [[interim--macro-for-holistically-updating-filebasename-macro,cf.-MUID-181,nb.-MUID-184,ver.-v0.0.2]]
	- [[macro-for-updating-meta-heading-endpoints,vis-Noteshippo,nb.-MUID-152,ver-v0.0.2]]
- **inserts**
	- [[macro-for-insert-of-all-inlink-endpoint,uti.-inline-dql,cf.-MUID-128,nb.-MUID-150,ver.-0.0.5]]
	- [[macro-for-inserting-automatic-toc,nb.-MUID-148,cf.-MUID-146,ver.-v0.0.3]]
	- [[macro-for-inserting-base-filepath,nb.-MUID-161,ver.-v0.0.6]]
	- [[macro-for-inserting-citum,nb.-MUID-191,ver.-v0.0.7]]
	- [[macro-for-inserting-file-basename,nb.-MUID-181,ver.-v0.0.7]]
	- [[macro-for-inserting-iherdc-template,vis-Characterization]]
	- [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]]
	- [[macro-for-inserting-toc-with-note-name,nb.-MUID-149,ver-v0.0.1]]
- **interim**
	- [[∑--macro-insert-inlink-heading-api,nb.-titled-with-macro,nb.-v0.0.1]]
	- [[∑--macro-yaml-update-of-tv-series-frontmatter,nb.-MUID-3136]]
	- [[interim--macro-for-bumping-doc-version-frontmatter-property-value,nb.-semver-patch,nb.-MUID-141]]
	- [[interim--macro-for-bumping-template-version-frontmatter-property-value,nb.-semver-patch,nb.-MUID-153]]
	- [[interim--macro-for-choice-prompted-kanban-root-label-insertion,nb.-MUID-197,ver.-0.0.1]]
	- [[interim--macro-for-inserting-abstract-emoji-tocs]]
	- [[interim--macro-for-inserting-doc-log,nb.-MUID-3120]]
	- [[interim--macro-for-inserting-organizing-resource-subdivisions,ver.-v0.0.1,vis-Writing]]
	- [[interim--macro-for-keyboard-shortcut-bullet-guide,nb.-MUID-203,ver.-0.0.1]]
	- [[interim--macro-for-updating-longform-title-using-muid-and-STORY_TITLE,nb.-MUID-145]]
	- [[interim--macro-inserting-private-lc-citum]]
	- [[interim--macro-inserting-query-for-targetted-text-in-h2-links]]
	- [[interim--macro-sluicing-unique-lcsh-headings-and-unclassified-notes,ad-hoc.-proper-lcsh-assignment,nb.-MUID-202,cf.-MUID-198]]
	- [[interim--macro-to-toggle-colorgrammar-in-cssclasses-yaml-field,nb.-MUID-3117]]
	- [[interim--macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-0.0.1]]
	- [[macro-for-inserting-noteshippo-private-header-api-endpoint,nb.-MUID-151,ver.-v0.0.2]]
	- [[macro-for-prompted-update-of-longform-drafttitle,nb.-MUID-140]]
- [[macro-for-inserting-comment-outs,uti.-templater-plugin,vis-Obsidianmd-app,nb.-MUID-180,ver.-v0.0.2]]
- [[macro-for-lcsh-heading-field-query-and-scrape-v1.0.2,uti.-MUID-1934]]
- [[macro-for-prompted-lcsh-specced-note-template,nb.-MUID-142,nb.-v0.0.10]]
- [[macro-for-prompted-scraping-for-specific-filename-using-embedded-query,nb.-v0.0.2,uti.-MUID-1934A]]
- [[macro-for-rating-books]]
- [[macro-for-scraping-transient-local-citations-and-resources,nb.-MUID-3123]]
- [[macro-for-sluicing-out-waypoints]]
- [[macro-for-stratagem-details]]
- [[macro-for-targetting-note-seeds]]
- [[macro-for-targetting-Subject-seeds]]
- [[macro-for-vocabulary-details,by-emoji]]
- **wips**
	- [[∑.≠.ø--macro-for-eec-tline]]
	- [[≈-testing-multiple-async-fires-executing-sequentially-within-on_all_templates_executed,nb.-templater-plugin]]

%% End Waypoint %%

# ---Transient
