---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID') %>
TEMPLATE_VERSION: v1.0.1
TEMPLATE_SOURCE: "[[10--bridge-spec-template]]"
UMID: 
tags:
  - _wip
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

> [!Goal] %%  %% GOAL
> This [[,aka-bridge-specced-note]] goal is to 

# =

**file_basename**: *`= this.file.name`* ***doc**-`=this.DOC_VERSION`*
**is-using-latest-template**: `= (([[10--bridge-spec-template]].TEMPLATE_VERSION)=(this.file.frontmatter.TEMPLATE_VERSION)) `

## Prerequisites

## Key Differences
## Key Similarities

## Analysis


<%* /** TEMPLATE VERSION LOG
- v1.0.1 
  - add a template log
**/ 
-%>