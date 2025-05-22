---
CREATION_DATE: <% await tp.file.creation_date("YYYY-MM-DD")%>
TEMPLATE_SOURCE: "[[10--library-spec-template]]"
TEMPLATE_VERSION: v1.0.5
tags:
  - _misc/_wip
PROJECT_PARENT: 
DEPENDENCIES:
  - "[[,aka-MUID-147]]"
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

* [[#10÷About]]
* [[#LR--TOC|TOC]]
	* [[~view-for-creating-dictionary-lists-with-transcluded-datum,vis-Dataviewjs,nb.-MUID-1022#=|ADL-TOC]]




# ---Transient Local Resources

## LR--TOC

```toc
maxLevel: 3
minLevel: 2
exclude: /^((\d+÷)|÷?(LR--)|÷?(LC--))/
```



# ---Transient

<%*/**
* v *2025-05-05*
	* Update the toc about
* v1.0.5 *2025-05-03*
	* Update private heading api
* v1.0.4 *2025-02-24*
	* Replace UMID w/ PROJECT_PARENT in frontmatter
	* Add about/toc/adl helper links (linking it relatively) so the template uses the target context rather than template note context.
	* Add collapsible meta api endpoint
	* Update basefilepath to v0.0.6
	* Update 20-Inlink to v0.0.5
	* Update basefilepath to v0.0.3
* v1.0.3 *2025-01-31*
  * remove dynamically populated TOC because it hardcodes
    * [[macro-for-inserting-toc-with-note-name,nb.-MUID-149,ver-v0.0.1]] is too dynamic.
    * [ ] Create indicator that this macro cannot be used in template. Must be manually activated. ➕ 2025-01-31 #_todo/to-add/upon-noteshippo-title-level-affix 
* v1.0.2 *2025-01-25*
  * Capitalize TOC, basefilepath to v.0.02
  * Add Inlink section v0.0.4
* v1.0.1 *2025-01-15*
	* Add creation date to metadata
	* Conform to shared noteshippo standards (basefilepath and TOC support)
	* Share the About Page easier
**/_%>
