---
TEMPLATE_VERSION: "v1.0.7_sourced-book-template"
<%*
/*
TEMPLATE_COMMITS: [
    "1.0.7 Rename template"
    "1.0.5 BUGFIX: Banner plugin to stupid to understand quoteless yaml",
    "1.0.4 Update template to nts_v1",
    "1.0.3: standardization to dashes",
    "1.0.2: Unify extraneous template data fields, intro commits, conform template look",
]
*/
%>
MUID: "<% await app.insertIncrementalId('MUID') %>"
CREATION_DATE: "<% tp.file.creation_date("YYYY-MM-DD") %>" 
tag:
  - _wip
  - _book
UMID: null
title: "{{title}}"
author: ["{{author}}"]
publisher: "{{publisher}}"
publish: "{{publishDate}}"
total: "{{totalPage}}"
isbn: ["{{isbn10}}", "{{isbn13}}"]
BANNER: "{{coverUrl}}"
STATUS: "unread"
category: "{{category}}"
subtitle: "{{subtitle}}"
---

# -

![[~view-for-local-tasks-using-a-progress-bar-MUID-698#=|nlk]]

```dataview
TASK where file.name = this.file.name and !completed
```

```dataview
TASK where file.name = this.file.name and completed
```

## Reference
* ∫ 

## Cover

![cover|150]({{coverUrl}})

# =



# ---Transient

[[~interim_view-for-recent-reference-link-to-note-title-transform]]

## Ω