---
BANNER:
  - "{{coverUrl}}"
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
MUID: <% await app.insertIncrementalId("MUID") %>
PERSONAL_RATING: 
STATUS: unread
TEMPLATE_VERSION: v1.0.10
TEMPLATE_SOURCE: "[[20--sourced-book-template]]"
UMID: 
author:
  - "{{author}}"
category: "{{category}}"
isbn:
  - "{{isbn10}}"
  - "{{isbn13}}"
publisher:
  - "{{publisher}}"
publish: "{{publishDate}}"
subtitle: "{{subtitle}}"
tags:
  - _wip
  - _book
title: "{{title}}"
total: "{{totalPage}}"
---

# -

## Meta

![[~view-for-local-tasks-using-a-progress-bar-MUID-698#=|nlk]]

```dataview
TASK where file.name = this.file.name and !completed
```

```dataview
TASK where file.name = this.file.name and completed
```

## About

> [!info] Hover over me [[~view-for-recent-reference-link-to-note-title-transform]] and copy normalized note title.

> [!info] See [[guide-to-personal-rating,cf.-Kepano]] to understand the rating system behind PERSONAL_RATING in frontmatter.
>
### Reference

* ∫

# =

# ---Transient Jobs

![[~viewfn-for-sluicing-header-links-for-citations-MUID-1560#=|?search_term=---Transient Local&t=nlknoui-scroll]]

# ---Transient Local Citations

---

---

# ---Transient Local Resources

<%*
/*
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
