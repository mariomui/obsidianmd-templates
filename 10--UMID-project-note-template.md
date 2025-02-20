---
CREATION_DATE: <% await tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
TEMPLATE_VERSION: v1.0.10
TEMPLATE_SOURCE: "[[10--UMID-project-note-template]]"
UMID: <% await app.templaterAddOnFig.addUuid() %>
aliases: 
tags:
  - _wip
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

- ! DO NOT confuse UMIDs with project notes as UMIDS are only there to facilitate projects that require different files with different names to be organized under one roof.
	- For instance, if i wanted to write a book, it would take in all the things tagged with a specific UMID. This way, I don't get bombarded.
### 11-Reference

> [!info] Hover over [[~view-for-referencing-current-jumpid]] for jumpid alias

* †

# =

**base_filepath**: *`= this.file.name`* doc-`=this.DOC_VERSION` `= this.MUID`/`=this.heading`/`=this.UMID`/






# ---Transient Commit Log

<%* /**
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
