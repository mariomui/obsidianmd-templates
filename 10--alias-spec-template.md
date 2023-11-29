---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% /** await app.insertIncrementalId('MUID') **/%>
SOURCE_TEMPLATE: '[[10--alias-spec-template]]'
TEMPLATE_VERSION: v1.0.7
UMID:
alias: 
tags: _wip
---

# -

# =

**filename:** `=this.file.path`

* This [[,aka-alias-specced-note]] points to:
  *

# ---Transient Local Resources

<%* /**
* COMMIT LOG FOR TEMPLATE
* v1.0.8
  * Remove UMID addUID because not all templates require a uuid
    * It gives a false impression that there is an external github link to the code when there might never be any.
    * In fact it makes more sense to create a bridge note to link all the specs together.
* v1.0.7
  * Add the template name to its own fm field as a link
  * Remove the template name from TEMPLATE_VERSION
* v1.0.6
  * revert DOC version to 0.0.0
  * Add templaterAddOnFig to addUuid
* v1.0.5 Rename tag to tags to fit convention
**/ %>
