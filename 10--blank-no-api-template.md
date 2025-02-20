---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
TEMPLATE_VERSION: v1.0.9
TEMPLATE_SOURCE: "[[10--blank-no-api-template]]"
UMID: 
aliases: 
tags:
  - _wip
---

# -

## 10-About

> [!info] %%  %% Goal
> 

# =

**base_filepath-v0.0.3**: *`= this.file.path`* doc-`= this.DOC_VERSION` / ids: `= this.MUID`,`= this.UMID` / lcsh: `= this.heading`





# ---Transient Local Resources

# ---Transient

<%* /**
- # ---Transient Template About
  * This template is the defacto template to use when no template is suitable.
  * Many [[,aka-index-specced-note]]s are created in this fashion. It is the most barebones template that is tracked with MUID.
  * For a template without MUID tracking see [[10--nascent-spec-template]] .
**/ %>

<%* /**
- # ---Transient Template Commit Log
  * v1.0.9 *2025-02-19*
    * Normalize About api
    * Normalize base filepath info
  * v1.0.8
    * Replace "filepath" with "base_filepath ([[internal-guide-to-naming-filepaths,cf.-Kanzi]])
  * v1.0.7
    * Replace "filename" with "filepath"  
    * Use the italics/bold ui format
      * 🔎 **filepath:** *somepath*
    * Add a [[transient-endpoint,vis-Noteshippo-heading-api,]] to template.
  * v1.0.6
    * Add goal callout to the about endpoint
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




