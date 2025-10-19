---
aliases:
  - __README__templates
  - templates
tags:
  - _meta
DOC_VERSION: v0.0.1
---


# -

### About

* This note is a:
	* [[folder-page,vis-Noteshippo,]]
	* [[Library-spec,vis-Noteshippo-taxonomy,]]

# =

**base_filepath-v0.0.9**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT`,alias: *`= this.aliases`*,nb: *`=this.NOTA_BENE`* , authors: *`= this.authors`* / lcsh: `= link(this.heading)`

* @ Folder Pages
	* [[+macros]]
	- [[+Y30,hard-coded-within-plugin-setting-tab-templates,nb.-MUID-194]]
---
* @ 10s Macro-behaving templates
	* 💁These templates:
		* behave as macros,
		* populate the entire page,
		* has no intermediate force (such as plugins) utilizing these templates
		* are activated soley by the user, manually.
	* [[10--alias-spec-template]]
	* [[10--youtube-litnote-template]]
	* [[10--definition-note-template]]
	* [[10--blank-no-api-template]]
	* [[10--bridge-spec-template]]
	* [[10--nascent-spec-template]]
	* [[10--project-spec-template,nb.-MUID-192]]
		* [[should-template-note-titles-include-MUIDs-like-their-other-macro-brethren,vis-Noteshippo?]]
	* [[10--library-spec-template]]
	* [[10--litnote-template,nb.-MUID-155]]
	* [[10--longform-multi-scene-template,ad-hoc-Longform-Index]]
* @ 20s Templates Used By A Plugin
	* 💁: *these templates are tied to an plugin.*
	* [[20--default-meta-template]]
	* [[20--fleeting-notes-template]]
	* [[20--sourced-book-template]]
	* [[20--folder-spec-template]]
* @ WIP
	* [[∑--declarative-spec-template]]
	* [[20.interim--question-note-template]]
	* [[∑--experiment-template]]
* @ 90s
	* [[90--bootup]]
* @ Misc
	* [[~view-for-taking-videonotes-using-transcription-and-easy-timestamp-linking,nb.-MUID-154]]
	* [[try.html]]
* @ Macros
	* [[∑.macro-for-inserting-library-entry-bullet-guide,vis-Writeshippo]]
	* [[,aka-macro-MUID-3123]]
	* [[∑.≠.ø--macro-for-eec-tline]]
	* [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]]
	* [[macro-for-vocabulary-details,uti.-emoji]]
	* [[sandbox--≈-macro-to-add-end-date-to-existing-project-specced-note]]
* @ Zotlit
	* # Archive
		* [[zt-annot.eta.prev]]
		* [[zt-annot.etab]]
		* [[zt-annots.etab]]
		* [[zt-annot.new.eta]]
		* [[zt-annots.new.eta]]
		* [[zt-note.etab]]
		* [[zt-annots.prev.eta]]
		* [[zt-annots.v1.1.2.eta]]
		* [[Y_templates/zotero/readme]]
		* [[Y_templates/zotero/archived/zt-cite2.eta]]
		* [[orange.eta]]
		* [[zt-cite2.eta]]
	* # In use
		* [[zt-annot.eta]]
		* [[zt-annots.eta]]
		* [[zt-cite.eta]]
		* [[zt-colored.eta]]
		* [[zt-field.eta]]
		* [[zt-note.eta]]
* @ Canvas
	* [[seven-pt-structure-plotting-canvas-template.canvas]]
* @ Obsoleted Content
	* [[ø--hbstemplate-import-ibook-csv-hbs-with-heading.hbs]]
	* [[ø--tag-page-template]]
* [[ø--hbstemplate-ibook-import-ibook-csv-with-bullet]]
* [[ø--macro-for-commonly-used-file-and-filepaths-inserts]]
* [[ø--macro-for-sluicing-waypoint-links-into-jobs]]
* [[readme]]
# ---Transient Jobs

![[~viewfn-sluicing-out-waypoint-like-unprocessed-links,nb.-MUID-1643#=|?search_term=---Transient Local Waypoints&t=nlk]]

# ---Transient Local Waypoints

%% Begin Waypoint %%
- **[[+macros]]**
- **+note-specs**
- **[[+Y30,hard-coded-within-plugin-setting-tab-templates,nb.-MUID-194]]**
- [[10--alias-spec-template]]
- [[10--blank-no-api-template]]
- [[10--bridge-spec-template]]
- [[10--definition-note-template]]
- [[10--library-spec-template]]
- [[10--litnote-template,nb.-MUID-155]]
- [[10--nascent-spec-template]]
- [[10--project-spec-template,nb.-MUID-192]]
- [[10--youtube-litnote-template]]
- [[20--default-meta-template]]
- [[20--fleeting-notes-template]]
- [[20--folder-spec-template]]
- [[20--sourced-book-template]]
- [[20.interim--question-note-template]]
- [[90--bootup]]
- **experiments**
	- [[∑--experiment-template]]
	- [[sandbox--≈-macro-to-add-end-date-to-existing-project-specced-note]]
- **ø--archive**
	- [[ø--hbstemplate-ibook-import-ibook-csv-with-bullet]]
	- [[ø--macro-for-commonly-used-file-and-filepaths-inserts]]
	- [[ø--macro-for-sluicing-waypoint-links-into-jobs]]
	- [[ø--tag-page-template]]
	- [[try.html]]
- [[ø--hbstemplate-import-ibook-csv-hbs-with-heading.hbs]]
- **obsidian-canvas**
	- [[seven-pt-structure-plotting-canvas-template.canvas]]
- **staged**
	- **interim**
		- [[∑--declarative-spec-template]]
	- **wip**
- **zotero**
	- **archived**
		- [[zt-annot.eta.prev]]
		- [[zt-annot.etab]]
		- [[zt-annot.new.eta]]
		- [[zt-annots.etab]]
		- [[zt-annots.new.eta]]
		- [[zt-annots.prev.eta]]
		- [[zt-annots.v1.1.2.eta]]
		- [[zt-cite2.eta]]
		- [[zt-note.etab]]
	- [[orange.eta]]
	- [[readme]]
	- [[zt-annot.eta]]
	- [[zt-annots.eta]]
	- [[zt-cite.eta]]
	- [[zt-colored.eta]]
	- [[zt-field.eta]]
	- [[zt-note.eta]]

%% End Waypoint %%

# ---Transient Commit Log

[[transient-commit-log-endpoint,bt.-Noteshippo-heading-api,]]
<%* /**
* DOC LOG
	* v0.0.2 Clusterize the waypoints
	* v0.0.1 Add jobs codelet to waypoints
**/-%>
