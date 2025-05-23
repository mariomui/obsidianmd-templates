---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID') %>
TEMPLATE_VERSION: v1.0.3
TEMPLATE_SOURCE: "[[10--bridge-spec-template]]"
PROJECT_PARENT: 
tags:
  - _misc/_wip
---

# -

## 00-Meta

> [!info]+ Progress Bar
> > ![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|olk]]
> ```dataview
> task where file.name = this.file.name and !completed
> ```
> > 
> ```dataview
> task where file.name = this.file.name and completed
> ```

### 10÷About

> [!Goal] %%  %% GOAL
> This [[,aka-bridge-specced-note]] goal is to 

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`


* [[##10÷About|10÷About]]
- [[##LR--TOC|TOC]]
## Prerequisites



## Key Differences
## Key Similarities

## Analysis



# ---Transient Local Resources

## LR--TOC

```toc
maxLevel: 3
minLevel: 2
exclude: /^((\d+÷)|÷?(LR--)|÷?(LC--))/
```

# ---Transient

<%* /** TEMPLATE VERSION LOG
- v1.0.4 *2025-05-07*
	- Update meta heading endpoints
	- update toc
- v1.0.3 *2025-01-18*
	- conform to use TOC
	- Update to use collapsible meta ep
- v1.0.2
	- Normalize the public api to standards
- v1.0.1 
  - add a template log
**/ 
-%>