---
CREATION_DATE: <% await tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
TEMPLATE_VERSION: v1.0.4
TEMPLATE_SOURCE: "[[10--youtube-litnote-template]]"
UMID: 
aliases: 
tags:
  - _wip
---

# -

## About

* This [[,aka-reference-specced-note|aka-literature-specced-note]] collects citations. It is combined with an Analysis portion that works as a temporary [[,aka-index-specced-note]] giving us some context to the information, namely what was collected, and how it relates to other notes, as well as other concepts in the same [[literature-note,etc]]


> [!info] Hover over me [[~view-for-recent-reference-link-to-note-title-transform]] and copy normalized note title.

### Reference

> [!info] Hover over [[~view-for-referencing-current-jumpid]] for jumpid alias

* √ 

#### TLDR Reference

* 


# =


## Control

![[helpercode-to-take-videonotes-using-transcription-and-easy-timestamp-linking#Transcript Control|nlk]]


## Analysis

* # Youtube Link
  * [[10--youtube-litnote-template#LR--Youtube Timestamp Notes Link|LR--Youtube Timestamp Notes Link]]

# ---Transient Jobs

![[~viewfn-for-sluicing-header-links-for-citations-MUID-1560#=|?search_term=---Transient Local&t=nlknoui-scroll]]

# ---Transient Local Citations

---

> [!example] `## LC--citum-t...`
* @ (⌘ shift ;) <-- timestamp wrapper for citations

---




# ---Transient Local Resources

## LR--Youtube Timestamp Notes Link

* See [[timestamp-notes-plugin,bt.-Obsidianmd-app,]] for usage.

```Place-youtube-url-in-me: timestamp-url
```

# ---Transient

<%*
/* Template Version Commit Log
* "1.0.4"
  * conform to a simpler header for LR notes link
- "1.0.3"
  - hardcode callout for reminding how to do timestamp wrapper.
- "1.0.2"
  - Add hover callouts for jumpid and note title transform
  - Add spacing for citation spacing
  - Add division spacers
  - Add LR remote link to share hard link so remote notes can open video player
  - Add temporary fix on api sharing video opener
*/
%>
