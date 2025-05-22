---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
PROJECT_PARENT: 
TEMPLATE_SOURCE: "[[10--blank-no-api-template]]"
TEMPLATE_VERSION: v1.0.10
aliases: 
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

### 11÷Reference

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`







# ---Transient Local Resources

# ---Transient

<%* /** Readme
  * This template is the defacto template to use when no template is suitable.
  * Many [[,aka-index-specced-note]]s are created in this fashion. It is the most barebones template that is tracked with MUID.
  * For a template without MUID tracking see [[10--nascent-spec-template]].
**/_%>
<%_* /** Transient Template Commit Log
* v1.0.10 *2025-05-03*
	* Normalize private endpoint
	* Update basefp to v0.0.6
	* Replace UMID with PROJECT_PARENT
* v1.0.9 *2025-02-19*
	* Normalize About api
	* Normalize base filepath info
* v1.0.8
	* Replace "filepath" with "base_filepath ([[∑--¡-titling,nb.-Noteshippo-title-level-affix]])
* v1.0.7
	* Replace "filename" with "filepath"  
	* Use the italics/bold ui format
		* 🔎 **filepath:** *somepath*
	* Add a [[transient-endpoint,vis-Noteshippo-heading-api,]] to template.
* v1.0.6
	* Add goal callout to the about endpoint
* v1.0.5
	* change front matter tag to tags to fit obsidian convention
	* Change the doc version from starting at 0.0.1 to 0.0.0
* v1.0.4
	* Conform the frontmatter to the other templates
* v1.0.3
	* Display filepath instead of just the name.
* v1.0.2
	* Add a filename to provide the thinker with the filename, reducing the need to remember the context since the hover window can sometimes block the name that is hovered.
**/ _%>



