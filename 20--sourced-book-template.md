---
BANNER: "{{coverUrl}}"
BANNER_y: 0
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
MUID: <% await app.insertIncrementalId("MUID") %>
PERSONAL_RATING: 
STATUS: unread
TEMPLATE_SOURCE: "[[20--sourced-book-template]]"
TEMPLATE_VERSION: v1.1.0
UMID: 
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
  - _wip
  - _book
title: "{{title}}"
total: "{{totalPage}}"
---

# -

## 00-Meta

![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|nlk]]

```dataview
TASK where file.name = this.file.name and !completed
```

```dataview
TASK where file.name = this.file.name and completed
```

## 11-About

> [!info] Hover over me [[~view-for-recent-reference-link-to-note-title-transform,nb.-MUID-115]] and copy normalized note title.

> [!info] See [[guide-to-personal-rating,cf.-Kepano]] to understand the rating system behind PERSONAL_RATING in frontmatter.
>
### 11-Reference

* ∫

## 20-Inlink


> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.4)
> * ℹ Commit/design logs are located in this [[π-lists-all-inlinks,nb.-MUID-128|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 20, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

**base_filepath-v0.0.2**: *`= this.file.path`* doc-`= this.DOC_VERSION` / ids: `= this.MUID`,`= this.UMID` / lcsh: `= this.heading` / updated on: `= dateformat(this.file.mday, "yyyy-LL-dd")` / file-size: `= round(this.file.size/1024,2)` KB


# ---Transient Jobs

![[~viewfn-for-sluicing-header-links-for-citations-MUID-1560#=|?search_term=---Transient Local&t=nlknoui-scroll]]

# ---Transient Local Citations

---

---

# ---Transient Local Resources

<%*
/*
- "v1.1.0"
	- conform basefilepath, conform meta and other headers to ordinality
	- and inlink api
	- change banner to a single string because pixel banner doesnt support arrays
- "1.0.10"
  - Add Meta H2
- "1.0.9"
  - Separate template version and source template
  - Sort frontmatter alphabetically
- "1.0.8" Update template to use transient jobs system
- "1.0.7 Rename template"
- "1.0.5 BUGFIX: Banner plugin to stupid to understand quoteless yaml",
- "1.0.4 Update template to nts_v1",
- "1.0.3: standardization to dashes",
- "1.0.2: Unify extraneous template data fields, intro commits, conform template look",
*/
%>