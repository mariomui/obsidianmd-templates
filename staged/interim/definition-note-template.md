---
TEMPLATE_VERSION: v1.0.5
MUID: <% await app.insertIncrementalId('MUID')%>
CREATION_DATE: 2024-03-02
tags:
  - _wip
UMID: 
TEMPLATE_SOURCE: "[[definition-note-template]]"
---

# -
## 10-About

> [!Goal] %%  %% GOAL
> This [[,aka-definition-specced-note]] goal is to 


### 11-Reference



# =

**base_filepath**: `= this.file.path` ***doc**-`=this.DOC_VERSION`*
**is-using-latest-template**: `= (([[definition-note-template]].TEMPLATE_VERSION)=(this.file.frontmatter.TEMPLATE_VERSION)) `

## Summary

**file_basename**: *`=this.file.name`*



# ---Transient

> [!info] Please use the following standard H2s as the apis.
> * Additional apis can be found in [[internal-guide-to-definition-note-specification,vis-Noteshippo]]

- ## Elements
- ## Examples And Counter Examples
- ## Implementation
- ## Tradeoffs†

† There are nested api endpoints in the [[Definition-spec,vis-Noteshippo-taxonomy,]]


---

<%* /** 
- # ---Transient Template About
  - This commented-out About page is to provide a [[,aka-thinking-surface|aka-thought-surface]] for improvements to the template.
  - @ *Should I record doc changes?*
    - [[,aka-definition-specced-note]]s,
      - changes too frequently for  [[transient-doc-log-endpoint,bt.-Noteshippo-heading-api,]] to be useful. 
        - 🤔 The note would get very lengthy. The core goal for these notes is to offer its knowledge.
**/ -%>

<%* /** 
- # ---Transient Template Commit Log
  - v1.0.5 *2024-07-01*
    - Add JD numbering to the - endpoint resources so that the alphabetic heading ordering doesn't wrongly rearrange them.
    - Add dql hard coded template version check 
  - v1.0.4 *2024-06-03*
    - Graduate interim to official usage
  - v1.0.3 *2024-05-14*
    - Change the ui color of the base_filepath value to contrast, giving a visual cue to what is a pathed base and an unpathed base (vis file metadata)
  - v.1.0.2 *2024-05-13*
    - Move interim template into interim folder
    - Add a commit log under Transient Template Commit Log endpoint
      - templates can't have their own ---Transient header because Transient headers would 
    - Remove the H1s for the Template About and Template Commit Log and replace with bullet pointed versions.
**/ -%>