---
CREATION_DATE: <% await tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
TEMPLATE_VERSION: v1.0.6
TEMPLATE_SOURCE: "[[10--default-template]]"
UMID: <% await app.templaterAddOnFig.addUuid() %>
aliases: 
tags:
  - _wip
---

# -

## Meta

![[~view-for-local-tasks-using-a-progress-bar-MUID-698#=|olk]]

```dataview
TASK WHERE file.name = this.file.name AND !completed
```
```dataview
TASK WHERE file.name = this.file.name AND completed
```

## About

> [!info] Hover over me [[~view-for-recent-reference-link-to-note-title-transform]] and copy normalized note title.
### Reference

> [!info] Hover over [[~view-for-referencing-current-jumpid]] for jumpid alias

* †

# =

**filepath**: *`= this.file.path`*



# ---Transient Commit Log

<%* /**

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
