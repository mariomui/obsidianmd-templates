---
TEMPLATE_VERSION: v1.0.10
MUID: <% await app.insertIncrementalId('MUID')%>
CREATION_DATE: 2024-03-02
tags:
  - _wip
UMID: 
TEMPLATE_SOURCE: "[[10--definition-note-template]]"
DOC_VERSION: v.0.0.1
---


# -
## 10-About

> [!Goal] %%  %% GOAL
> This [[,aka-definition-specced-note]] goal is to 


## 11-Reference


## 20-Inlink


> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.4)
> * ℹ Commit/design logs are located in this [[π-lists-all-inlinks,nb.-MUID-128|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 20, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

**base_filepath-v0.0.2**: *`= this.file.path`* doc-`= this.DOC_VERSION` / ids: `= this.MUID`,`= this.UMID` / lcsh: `= this.heading` / updated on: `= dateformat(this.file.mday, "yyyy-LL-dd")` / file-size: `= round(this.file.size/1024,2)` KB



## Abstract

**file_bn--v.0.0.3**: *`= this.file.name`* doc-`=this.DOC_VERSION` `= this.MUID`/`=this.heading`/`=this.UMID`/




> [!tip] See [[#Elements]]


## Elements





---

# ---Transient

> [!info]+ Please use the following standard H2s as the apis.
> * Additional apis can be found in [[internal-guide-to-definition-note-specification,vis-Noteshippo]]
> > ## Elements
> > ## Examples And Counter Examples
> > ## Implementation
> > ## Tradeoffs†
> † There are nested api endpoints in the [[Definition-spec,vis-Noteshippo-taxonomy,]]

---

# ---Transient

<%* /** 
- # ---Transient Template About
  - This commented-out About page is to provide a [[,aka-thinking-surface|aka-thought-surface]] for improvements to the template.
  - @ *Should I record doc changes?*
    - [[,aka-definition-specced-note]]s,
      - changes too frequently for  [[transient-doc-log-endpoint,bt.-Noteshippo-heading-api,]] to be useful. 
        - 🤔 The note would get very lengthy. The core goal for these notes is to offer its knowledge.
      - And yet i think doc versions could help provide specific mile stones to a document. A significant knowledge update from its etc or primary source could mean an update.
**/ -%>

<%* /** 
- # ---Transient Template Commit Log
  - v1.0.10 *2025-02-08*
    - Rename Summary api to abstract api
    - Rename the endpoints under - with prefixed ordinality
  - v1.0.9 *2025-02-06*
    - Add Elements link to Summary
      - Make sure its easy to see using the callouts feature
  - v1.0.8
    - Add Transient Scrapwork Api
    - Add Inlink Api
  - v1.0.7
    - change the base_filepath to include doc id, muid, and the lcsh heading
    - remove the template check because of fragility
    - make sure the file basename has versioning
  - v1.0.6 *2024-11-28*
    - Add Doc version into metadata
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