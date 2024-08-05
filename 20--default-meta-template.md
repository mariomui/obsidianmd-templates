---
TEMPLATE_VERSION: v1.0.1
MUID: <% await app.insertIncrementalId('MUID') %>
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
tags:
  - _meta
UMID: 
TEMPLATE_SOURCE: "[[20--default-meta-template]]"
---





# -
## About

* ℹ Template should be used when any administrion note, or dashboard note is created.  (DELETE ME AFTER READING)

# =





# ---Transient

<%* /**

![[~view-for-local-tasks-using-a-progress-bar-MUID-698#=|nlk]]

```dataview
task where file.name = this.file.name and !completed
```

```dataview
task where file.name = this.file.name and completed
```

- [ ] Consider adding `#_noteshippo/note-spec/dashboard-view` to note specs ➕ 2024-05-03 #_todo/to-muse/upon-noteshippo-note-spec  
**/ -%>
