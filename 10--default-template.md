---
CREATION_DATE: <% await tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.1
MUID: <% await app.insertIncrementalId('MUID')%>
TEMPLATE_VERSION: v1.0.5_default-template
UMID: <% await app.templaterAddOnFig.addUuid() %>
alias: 
tags:
  - _wip
---

# -

![[~view-for-local-tasks-using-a-progress-bar-MUID-698#=|olk]]

```dataview
TASK WHERE file.name = this.file.name AND !completed
```
```dataview
TASK WHERE file.name = this.file.name AND completed
```

## About

* Hover over me and snatch the output of note title algorithm:[[~view-for-recent-reference-link-to-note-title-transform]]

### Reference

![[~view-for-referencing-current-jumpid#=|nlk]]

* †

# =

*`= this.file.name`*
![[~view-for-calculating-reading-time#=|olk ui-noscroll]]

# ---Transient Commit Log

<%* /**

v0.0.1 Add a new line after jumpid codelet for better contrast on reflink

**/ -%>
