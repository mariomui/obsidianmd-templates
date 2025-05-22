---
CREATION_DATE: "2024-05-12"
MUID: MUID-2298
PROJECT_PARENT: 
TEMPLATE_SOURCE: "[[∑--experiment-template]]"
TEMPLATE_VERSION: v1.0.1
tags:
  - _meta
---

# -
## 00-Meta

> [!info]- Progress Bar v0.0.3
> > ![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|olk]]
> ```dataview
> task where file.name = this.file.name and !completed
> ```
> > 
> ```dataview
> task where file.name = this.file.name and completed
> ```


### 10÷About

- ? Should [[,aka-experiment-specced-note]]s merge with [[,aka-question_specced_note]]?
	- no, [[,aka-question-note-template]] isn't suitable for experiment notes. Qualitative templates and quantitative templates have different purposes.

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

* [[∑--experiment-template#10÷About|10÷About]]





# ---Transient

<%*/** Readme
* Based on [[10--definition-note-template]]
* This template shows how to do experiments.
**/_%>

<%* /** Commit Log
* v1.0.2 *2025-05-18*
	* Apply [[macro-for-updating-meta-heading-endpoints,vis-Noteshippo,nb.-MUID-152,ver-v0.0.2]] (v0.0.2)
	* Apply [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]] (v0.0.3)
	* Apply [[interim--macro-update-frontmatter-property-name,nb.-UMID-to-PROJECT_PARENT,nb.-MUID-3118,ver.-0.0.1]] (v0.0.1)
* v1.0.1
	* 
**/_%>