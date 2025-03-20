---
aliases:
  - __README___hard-coded-within-plugin-setting-tab-templates
TEMPLATE_VERSION: v1.0.0-folder-page
CREATION_DATE: 2023-06-17
tags:
  - _meta
  - _noteshippo/∑≠--v1-spec/_structural
UMID:
---

# -

[[Templater-plugin-for-obsidianmd-should-only-use-templates-from-a-single-assigned-folder,prima-facie]]

```dataview
task where file.name = this.file.name and !completed
```


## About


## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-lists-all-inlinks,nb.-MUID-128|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`



# =

**base_filepath-v0.0.4**: `= choice( contains(this.file.folder, this.file.name), link(this.file.name), join(["*",this.file.name,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,`= this.UMID` / lcsh: `= this.heading`


This folder houses all the templates that need to be manually added into the plugin settings;

Due to limitations of the API, I can only check the contents of the template against the plugin only when you visit the page.

# ---Transient

Should the dataview "List of templates hard coded within plugin settings v0.0.0" be colocated into a partial view?

```dataview
TABLE WITHOUT ID file.link as "List of templates hard coded within plugin settings v0.0.0"
WHERE startswith(file.path,this.file.folder)
LIMIT 50
```
