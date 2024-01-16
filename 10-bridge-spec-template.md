---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
DOC_VERSION: 
MUID: <% await app.insertIncrementalId('MUID') %>
TEMPLATE_VERSION: v1.0.0
TEMPLATE_SOURCE: "[[10-bridge-spec-template]]"
UMID: 
tags: _wip
---

# -

## Meta
![[~view-for-local-tasks-using-a-progress-bar-MUID-698#=|nlk]]

```dataview
task where file.name = this.file.name and !completed
```

```dataview
task where file.name = this.file.name and completed
```

## About


# =

*`= this.file.name`*
## Prerequisites

## Key Differences
## Key Similarities

---