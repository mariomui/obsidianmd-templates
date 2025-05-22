---
AutoNoteMover: disable
CREATION_DATE: <% tp.date.now("YYYY-MM-DD") %>
DOC_VERSION: v0.0.0
PROJECT_PARENT: 
TEMPLATE_SOURCE: "[[20--folder-spec-template]]"
TEMPLATE_VERSION: v0.0.4
aliases:
  - __README__<%tp.file.title%>
tags:
  - _misc/_wip
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

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`

# =

# --Transient Jobs

![[~viewfn-sluicing-out-waypoint-like-unprocessed-links,nb.-MUID-1643#=|?search_term=---Transient Local Waypoints#=|nlk]]

# ---Transient Local Waypoints

%  Waypoint %%

# ---Transient

<%* /**
* v0.0.4 *2025-05-16*
	* Set a flag in the yaml to prevent automover plugin from moving folder notes away from their folder.
* v0.0.3 *2025-03-16*
	* Remove meta tag 
* v0.0.2 *2025-02-19*
	* *2025-02-19* Add folder page template to yml field
* v1.0.2 *2025-01-06*
  * This is tied to [[folder-notes-plugin,bt.-ObsidianMD-app,]]
* v1.0.1 Add commit log
**/ -%