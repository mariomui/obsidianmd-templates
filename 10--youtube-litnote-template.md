---
CREATION_DATE: <% await tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID')%>
TEMPLATE_VERSION: v1.0.6
TEMPLATE_SOURCE: "[[10--youtube-litnote-template]]"
PROJECT_PARENT: 
aliases: 
tags:
  - _misc/_wip
authors: 
DEPENDENCIES:
---

# -

## 00-Meta

> [!info]+ Progress Bar
> > ![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|olk]]
> ```dataview
> task where file.name = this.file.name and !completed
> ```
> > 
> ```dataview
> task where file.name = this.file.name and completed
> ```
### 10÷About

* This [[,aka-reference-specced-note|aka-literature-specced-note]] collects citations. It is combined with an Analysis portion that works as a temporary [[,aka-index-specced-note]] giving us some context to the information, namely what was collected, and how it relates to other notes, as well as other concepts in the same [[literature-note,etc]]


> [!info] Hover over me [[~view-for-recent-reference-link-to-note-title-transform,nb.-MUID-115]] and copy normalized note title.

### 11÷Reference

> [!info] Hover over [[~view-for-referencing-current-jumpid]] for jumpid alias

* √ 


## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`



# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`



## 00-Control

![[~view-for-taking-videonotes-using-transcription-and-easy-timestamp-linking,nb.-MUID-154#Transcript Control|nlk]]


## Analysis

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`



* # Youtube Link
  * [[10--youtube-litnote-template#LR--Youtube Timestamp Notes Link|LR--Youtube Timestamp Notes Link]]

# ---Transient Jobs

![[~viewfn-for-sluicing-header-links-for-citations,nb.-MUID-1560#=|?search_term=---Transient Local&t=nlknoui-scroll]]

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
* v1.0.5
  * Replace commonly used file base paths with one that includes doc version
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
