---
alias:
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
tag: _wip 
TEMPLATE_VERSION: v1.0.4_blank-template
UMID: 
---

# -

## About

# =

**filename:** `=this.file.path`


# ---Transient Local Resources

<%* /**
* COMMIT LOG
  * v1.0.4
    * Conform the frontmatter to the other templates
  * v1.0.3
    * Display filepath instead of just the name.
  * v1.0.2
    * Add a filename to provide the thinker with the filename, reducing the need to remember the context since the hover window can sometimes block the name that is hovered.
**/ %>