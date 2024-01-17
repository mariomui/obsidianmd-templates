---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
TEMPLATE_VERSION: v1.0.5
TEMPLATE_SOURCE: "[[10--blank-template]]"
UMID: 
aliases: 
tags:
  - _wip
---

# -

## About

# =

**filename:** `=this.file.path`

# ---Transient Local Resources

<%* /**
* COMMIT LOG
  * v1.0.5 
    * change front matter tag to tags to fit obsidian convention
    * Change the doc version from starting at 0.0.1 to 0.0.0
  * v1.0.4
    * Conform the frontmatter to the other templates
  * v1.0.3
    * Display filepath instead of just the name.
  * v1.0.2
    * Add a filename to provide the thinker with the filename, reducing the need to remember the context since the hover window can sometimes block the name that is hovered.
**/ %>
