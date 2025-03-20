---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID') %>
TEMPLATE_SOURCE: "[[10--alias-spec-template]]"
TEMPLATE_VERSION: v1.1.0
UMID: 
aliases: 
tags:
  - _misc/_wip
---

# -

# =

**base_filepath-v0.0.3**: *`= this.file.path`* doc-`= this.DOC_VERSION` / ids: `= this.MUID`,`= this.UMID` / lcsh: `= this.heading`

---

* This [[,aka-alias-specced-note]] points to:
  * 


# ---Transient Local Resources

# ---Transient

<%* /**
* # ---Transient Template About
  * **file_basename**: *`= this.file.name`*
  * This alias template ....
  * Why do aliases need the template-version again?
**/ %>

<%* /**
* # ---Transient Template Commit Log
  * v1.1.0 *2025-02-26*
    * update base filepath to v0.0.3
  * v1.0.12 *2025-01-11*
    * Remove the template check because inline dataview is prone to fragility. Willing to live with template drift.
  * v1.0.11 *2024-05-28*
    * Add doc to versioning to explicitly state its usecase is to easily show that the consumed item comes from what version of the document not what version of the template.
  * v1.0.10 *2024-05-14*
    * Conform the template to follow [[transient-endpoint,vis-Noteshippo-heading-api,]] as it pertains to templates.
    * Add a [[transient-endpoint,vis-Noteshippo-heading-api,]]
    * Add dates along with the version in commit logs.
    * Update the template version to check the note if its using the latest template version or not.
    * Replace SOURCE_TEMPLATE to TEMPLATE_SOURCE
  * v1.0.9
    * add version template version to the public api
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
