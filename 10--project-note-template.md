---
CREATION_DATE: <% await tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID') %>
PROJECT_END_DATE: 
PROJECT_PARENT: "[[<% await tp.file.title %>]]"
TEMPLATE_SOURCE: "[[10--project-note-template]]"
TEMPLATE_VERSION: v1.0.11
aliases: 
tags:
  - _misc/_wip
---

# -

## 00-Meta

![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|olk]]

```dataview
TASK WHERE file.name = this.file.name AND !completed
```
```dataview
TASK WHERE file.name = this.file.name AND completed
```

## 10-About

> [!info] Hover over me [[~view-for-recent-reference-link-to-note-title-transform,nb.-MUID-115]] and copy normalized note title.

[[,aka-project-specced-note]]s have a desired product at the end, and a desired start and end date. 

<%* 
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
### 11-Reference

> [!info] Hover over [[~view-for-referencing-current-jumpid]] for jumpid alias

* †

# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`



# ---Transient Jobs

![[interim--~viewfn-for-sluicing-out-embedded-query-into-a-job-queue,nb.-MUID-1934#=|?t=nlk&search_term=[PROJECT_PARENT: <% title %>]]

# ---Transient Local Resources

## LR--query--files having heading with <% title %>

```query
[PROJECT_PARENT: <% title %>]
```




# ---Transient


<%* /**
- v1.0.11
	- PROJEcT PaTh field value must be a link and the title itself
	- automate the frontmatter link scrape
	- add project end date
	- update basefp to v0.0.6
	- remove commit log header
	- test out tp.file.title in frontmatter
	- remove UMID code
- v1.0.9
	- add the term project note to UMID
- v1.0.8
  - add commonly used macro that shows filepath and doc version
* v1.07
  * change the name to show that this template is a template that has UMID In it, meant for big projects.
* v1.0.6 
  * Add template source into metadata
  * Revert the DOC_VERSION to v0.0.0
  * Update filename to filepath in the public api
  * Conform tasks to be under the Meta h2
  * Remove the reading time partial dataview
  * Update the note title transform ~dataview to use callouts
  * Update the reference jumpid ~dataview to use callouts
* v1.0.5 Add a new line after jumpid codelet for better contrast on reflink

**/ -%>

e