---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
PROJECT_PARENT: 
TEMPLATE_SOURCE: "[[10--litnote-template]]"
TEMPLATE_VERSION: v0.1.4
aliases: 
authors: 
heading: 
tags:
  - _misc/_wip
---

---

# -

## 00-Meta

> [!info]+ Progress Bar
> > ![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|olk]]

```dataview
TASK WHERE file.name = this.file.name AND !completed
```

```dataview
TASK WHERE file.name = this.file.name AND completed
```


### 10-About

- This [[,aka-reference-specced-note|aka-literature-specced-note]]'s contains ...

> [!info] [[~view-for-recent-reference-link-to-note-title-transform,nb.-MUID-115#Normalized Reference|Hover over me and copy the properly formatted note title]]
> *Make sure that reference † is populated*

This note should be prefixed with [[†,bt.-Noteshippo-title-level-affix,]]
### 11-Reference

> [!info] Hover over me and copy the [[~view-for-referencing-current-jumpid#=|jumpid]]

* †

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-lists-all-inlinks,nb.-MUID-128|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`





# ---Transient Jobs

![[~viewfn-for-sluicing-header-links-for-citations,nb.-MUID-1560#=|?search_term=---Transient Local&t=nlk]]

# ---Transient Local Resources

# ---Transient Local Citations

## LC--

**file_bn--v0.0.4**: *`= this.file.name`* doc-`=this.DOC_VERSION` `= this.MUID`/`=this.heading`/`=this.UMID`/






# ---Transient

<%* /**
* v0.1.4 *2025-03-19*
	* change content in About api to suit current writing style
	* normalize meta to subsume about and reference
	* Use v0.0.6 of macro citum
	* update basefp to v0.0.6
	* replace UMID with PROJECT_PARENT
* v0.1.3 *2025-03-04*
	* update inlink to v0.0.5
* v0.1.2 *2025-02-10*
	* Add a hr line to avoid a bug where clicking untitled shifts the pageview
* v0.1.1 *2025-01-30*
  * add authors to yaml
* v0.1.0 *2025-01-25*
  * add inlinks view
  * conform basepath view
* v0.0.10
	* remove interim beause it reached 10 update points
	* add to file basename to have UMID and the heading so that it is easier to see what lcsh the file is by their preview
* v0.0.9
  * add JD to the template
* v0.0.8
  * Add a [[transient-endpoint,vis-Noteshippo-heading-api,]] to template
* v0.0.7
  * Update the about page to reflect the true note type. Replace "declaration spec note" with ",aka-reference-specced-note|aka-literature-specced-note"
  * change name of template to something shorter, from literature note to litnote template
* v0.0.6
  * add transient local resources endpoint
* v0.0.5
  * Switch the Transient Jobs partial to pick up Transient Local instead of Transient Local Citations
* v0.04
  * Update with adding a link, seperating version from template
  * start conforming to double dashes
  * Change Transient 010... to Transient Jobs
  * Change LC--citations-- to LC--citum--
  * Remove Reading time partial
* v0.03_litnote-template Update template with proper templater commenting out tags
* v0.02_litnote-template Update headings to be compatible with  [[~viewfn-for-sluicing-header-links-for-citations,nb.-MUID-1560]]
**/ -%>
