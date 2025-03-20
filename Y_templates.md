---
Aliases: ["__README__templates", templates]
tags: _noteshippo/∑≠--v1-spec/∑≠_structural-note
DOC_VERSION: v0.0.1
---

# -

## About

* This note is a:
  * [[folder-page,vis-Noteshippo,]]
  * [[Library-spec,vis-Noteshippo-taxonomy,]]

# =

**base_filepath-v0.0.5**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= this.heading`


- @ Folder Pages
	* [[_macros]]
	* [[_hard-coded-within-plugin-setting-tab-templates]]

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
  * [[10--project-note-template]]
  * [[10--library-spec-template]]
  * [[10--litnote-template]]
* @ 20s
  * 💁: *these templates are tied to an plugin.*
  * [[20--default-meta-template]]
  * [[20--evergreen_template]]
  * [[20--fleeting-notes-template]]
  * [[20--sourced-book-template]]
  * [[20--folder-page-template]]
* @ WIP
  * [[∑--declarative-spec-template]]
  * [[∑--experiment-template]]
* @ 90s
  * [[90--bootup]]
* @ Misc
	* [[helpercode-to-take-videonotes-using-transcription-and-easy-timestamp-linking]]
	* [[try.html]]
* @ Macros
  * [[macro-for-callout-like-detail]]
  * [[macro-for-citations]]
  * [[macro-for-eec-tline]]
  * [[macro-for-local-page-tasks]]
  * [[macro-for-vocabulary-details,by-emoji]]
  * [[merge_template]]
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
    * [[readme]]
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

# ---Transient Jobs

![[~viewfn-sluicing-out-waypoint-like-unprocessed-links,nb.-MUID-1643#=|?search_term=---Transient Local Waypoints&t=nlk]]

# ---Transient Local Waypoints

%% Begin Waypoint %%
- **[[_hard-coded-within-plugin-setting-tab-templates]]**
- **[[_macros]]**
- [[10--alias-spec-template]]
- [[10--blank-no-api-template]]
- [[10--bridge-spec-template]]
- [[10--definition-note-template]]
- [[10--library-spec-template]]
- [[10--litnote-template]]
- [[10--nascent-spec-template]]
- [[10--project-note-template]]
- [[10--youtube-litnote-template]]
- [[20--default-meta-template]]
- [[20--evergreen_template]]
- [[20--fleeting-notes-template]]
- [[20--folder-page-template]]
- [[20--sourced-book-template]]
- [[90--bootup]]
- **experiments**
	- [[∑--experiment-template]]
- **ø--archive**
	- [[helpercode-to-take-videonotes-using-transcription-and-easy-timestamp-linking]]
	- [[merge_template]]
	- [[ø--hbstemplate-ibook-import-ibook-csv-with-bullet]]
	- [[ø--tag-page-template]]
	- [[try.html]]
- [[ø--hbstemplate-import-ibook-csv-hbs-with-heading.hbs]]
- **obsidian-canvas**
	- [[seven-pt-structure-plotting-canvas-template.canvas]]
- **staged**
	- **wip**
		- [[∑--declarative-spec-template]]
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
