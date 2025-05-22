---
CREATION_DATE: 2023-06-17
PROJECT_PARENT: 
TEMPLATE_VERSION: v1.0.0-folder-page
aliases:
  - __README___hard-coded-within-plugin-setting-tab-templates
tags:
  - _meta
---

# -

[[prefer-colocating-frequently-modified-notes-such-as-noteshippo-templates,prima-facie]]

#_noteshippo/prima-facie/prefer
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


## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`



# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`


- This folder houses all the templates that need to be manually added into the plugin settings;

- ! Due to limitations of the API, data drift checking can only happen when visiting the note below.
	* [[note-refactor-template-with-manual-sync-alert]]
	* [[ø.≠--folder-page-template-with-manual-sync-alert]]

# ---Transient Jobs

![[~viewfn-sluicing-out-waypoint-like-unprocessed-links,nb.-MUID-1643#=|?search_term=---Transient Local Waypoint&t=nlk]]

# ---Transient Local Waypoint

> [!info] Insert Waypoint Marker below using `%%` `Waypoint` `%%`: 

%% Begin Waypoint %%
- [[note-refactor-template-with-manual-sync-alert]]
- [[ø.≠--folder-page-template-with-manual-sync-alert]]

%% End Waypoint %%

# ---Transient Local Resources



# ---Transient
