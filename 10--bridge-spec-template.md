---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID') %>
TEMPLATE_VERSION: v1.0.2
TEMPLATE_SOURCE: "[[10--bridge-spec-template]]"
UMID: 
tags:
  - _wip
---

# -

## 00-Meta

![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|nlk]]

```dataview
task where file.name = this.file.name and !completed
```

```dataview
task where file.name = this.file.name and completed
```

## 10-About

> [!Goal] %%  %% GOAL
> This [[,aka-bridge-specced-note]] goal is to 

# =

**base_filepath**: *`= this.file.path`* doc-`=this.DOC_VERSION` `= this.MUID`/`=this.heading`/`=this.UMID`/

* [[10--bridge-spec-template#10-About|10-About]]
* [[10--bridge-spec-template#LR--TOC|TOC]]
## Prerequisites



## Key Differences
## Key Similarities

## Analysis



# ---Transient Local Resources

## LR--toc
```toc
maxLevel: 2
minLevel: 2
```

# ---Transient

<%* /** TEMPLATE VERSION LOG
- v1.0.3 *2025-01-18*
	- conform to use TOC
- v1.0.2
	- Normalize the public api to standards
- v1.0.1 
  - add a template log
**/ 
-%>