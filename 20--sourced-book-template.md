---
BANNER: "{{coverUrl}}"
BANNER_y: 0
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
MUID: <% await app.insertIncrementalId("MUID") %>
PERSONAL_RATING: 
PROJECT_PARENT: 
STATUS: unread
TEMPLATE_SOURCE: "[[20--sourced-book-template]]"
TEMPLATE_VERSION: v1.1.2
author:
  - "{{author}}"
category: "{{category}}"
isbn:
  - "{{isbn10}}"
  - "{{isbn13}}"
publish: "{{publishDate}}"
publisher:
  - "{{publisher}}"
subtitle: "{{subtitle}}"
tags:
  - _misc/_wip
  - media/_book
title: "{{title}}"
total: "{{totalPage}}"
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

> [!info] Hover over me [[~view-for-recent-reference-link-to-note-title-transform,nb.-MUID-115]] and copy normalized note title.
> > -—- <-- Prefix the author manually in case auto transform failed.

> [!info] See [[guide-to-personal-rating,cf.-Kepano]] to understand the rating system behind PERSONAL_RATING in frontmatter.
>
	
### 11÷Reference

* ∫ 

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`





# ---Transient Jobs

![[~viewfn-for-sluicing-header-links-for-citations,nb.-MUID-1560#=|?search_term=---Transient Local&t=nlknoui-scroll]]

# ---Transient Local Citations



# ---Transient Local Resources

# ---Transient

<%* /** Template Commit Log
* v1.1.2 *2025-05-22*
	* Apply [[macro-for-updating-meta-heading-endpoints,vis-Noteshippo,nb.-MUID-152,ver-v0.0.2]] v0.0.2
	* Apply [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]] v0.0.3
	* Add -—- for manual titling
	* bump patch , template version
	* Replace UMID in frontmatter with PROJECT_PARENT , sort frontmatter alphabetically
- v1.1.1 *2025-03-06*
	- Update basefilepath to v0.0.6
	- Update basefilepath to v0.0.5
	- normalize the public api subendpoints
- v1.1.0
	- conform basefilepath, conform meta and other headers to ordinality
	- and inlink api
	- change banner to a single string because pixel banner doesnt support arrays
- 1.0.10
  - Add Meta H2
- 1.0.9
  - Separate template version and source template
  - Sort frontmatter alphabetically
- 1.0.8 
	- Update template to use transient jobs system
- 1.0.7 Rename template
- 1.0.5 BUGFIX: Banner plugin to stupid to understand quoteless yaml,
- 1.0.4 Update template to nts_v1,
- 1.0.3 standardization to dashes,
- 1.0.2 Unify extraneous template data fields, intro commits, conform template look",
**/ _