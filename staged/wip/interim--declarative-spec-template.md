---
CREATION_DATE: 2025-03-16
MUID: 
PROJECT_PARENT: 
TEMPLATE_SOURCE: "[[interim--declarative-spec-template]]"
TEMPLATE_VERSION: v0.0.1
tags:
  - _misc/_wip
---

# -


## 00-Meta

### 08 Tasks

![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|nlk]]

```dataview
task where file.name = this.file.name and !completed
```

```dataview
task where file.name = this.file.name and completed
```

### 10-About

- This [[,aka-declarative-specced-note]] construes ...

### 11-Reference

- †

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> >`= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`


## 005 Abstract

- [^abstract] 

## 010 Value

- [^value] 


## 030 Experiment

- [^experiment] 


## 050 Logic

- [^logic] 




# ---Transient

# ---Transient Local Z9 Footnotes

[^value]: * Explains the value of this claim.

[^abstract]: * A short abstract allows the reader to understand the the context of the claim, especially its source. Also allows an overview so that reader can easily disambiguate the pertinence of the prima facie.

[^experiment]: * shows my sandbox stuff to test out whether the claim is valid.

[^logic]: * Shows my approach and timeline of how the claim came to be.  🤔 Or how the experiment helps prove or disprove the theory (🔄s)