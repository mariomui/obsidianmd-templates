---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
TEMPLATE_VERSION: v0.0.9
TEMPLATE_SOURCE: "[[interim--litnote-template]]"
UMID: 
aliases: 
tags:
  - _wip
---

# -

## 00-Meta

![[~view-for-local-tasks-using-a-progress-bar-MUID-698#=|olk]]

```dataview
TASK WHERE file.name = this.file.name AND !completed
```
```dataview
TASK WHERE file.name = this.file.name AND completed
```


## 10-About

This [[,aka-reference-specced-note|aka-literature-specced-note]]'s contains...

> [!info] [[~view-for-recent-reference-link-to-note-title-transform,nb.-MUID-115#Normalized Reference|Hover over me and copy the properly formatted note title]]
> *Make sure that reference † is populated*
### 11-Reference

> [!info] Hover over me and copy the [[~view-for-referencing-current-jumpid#=|jumpid]]

* †

# =

**file_basename**: *`= this.file.name`* doc-`=this.DOC_VERSION` `= this.MUID`


# ---Transient Jobs

![[~viewfn-for-sluicing-header-links-for-citations-MUID-1560#=|?search_term=---Transient Local&t=nlk]]

# ---Transient Local Resources

# ---Transient Local Citations

## LC--citum--

**file_basename**: *`= this.file.name`* *doc-`=this.DOC_VERSION`*



# ---Transient

<%* /**
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
* v0.02_litnote-template Update headings to be compatible with  [[~viewfn-for-sluicing-header-links-for-citations-MUID-1560]]
**/ -%>