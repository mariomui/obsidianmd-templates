<%* 
let lcsh = await tp.system.prompt("What's the lcsh?");
_%>
---
TEMPLATE_VERSION: v0.0.3
TEMPLATE_SOURCE: "[[macro-for-prompted-lcsh-specced-note-template]]"
tags:
  - _wip
UMID: 
CREATION_DATE: <% tp.date.now("YYYY-MM-DD") %>
MUID:
---

# -

## 10-About

**file_basename--v.0.0.2**: *`= this.file.name`* doc-`=this.DOC_VERSION` `= this.MUID`/`=this.heading`/`=this.UMID`/

Notes assigned with "<% lcsh %>" denote ...

## 11-Reference

# =

**base_filepath-v0.0.3**: *`= this.file.path`* doc-`= this.DOC_VERSION` / ids: `= this.MUID`,`= this.UMID` / lcsh: `= this.heading`


> [!info]- About
> ![[#10-About|nlk]]



---




# ---Transient Jobs

![[interim--~viewfn-for-sluicing-out-embedded-query-into-a-job-queue,nb.-MUID-1934#=|?t=nlk&search_term=[heading: "<% lcsh %>"]]

# ---Transient Local Resources

## LR--query--files having heading with <% lcsh %>

```query
[heading: "<% lcsh %>"]
```



# ---Transient

<%*/**
Transient Template Doc Log
* v0.0.3 *2025-02-19*
	* normale basefilepath to v0.0.3
	* Add creation date to yaml
* v0.0.2 *2025-02-08*
	* Conform to base names
	* Make the about api more shareable by excising reference from it
		* let each individual note decide whether they want the nested api
	* Allow the user to see a collapsible about api content on hover
* v0.0.1 *2025-01-13*
	* Scrape for exact matches on the lcsh to avoid false positives
**/_%>

<%*
tp.hooks.on_all_templates_executed(async () => {
	const fileView = tp.app.workspace.getActiveFileView()
	const metadataEditor = fileView.metadataEditor
	let lcsh_tag = "#_lcsh/"
	const shouldManual = [" ","/","("].some((m) => {
		return lcsh.indexOf(m) > -1
	})
	let rhs = shouldManual;
	if (shouldManual) {
		rhs = await tp.system.prompt("What's the lcsh?")
	} else {
		rhs = lcsh
	}

	lcsh_tag += rhs.toLowerCase();

	const yaml = metadataEditor.serialize()
	yaml.tags.push(lcsh_tag)
	metadataEditor.synchronize(yaml)
	metadataEditor.save()

	fileView.editor.refresh()
	const cb = () => {
		this.app.commands.executeCommand(
			this.app.commands.commands["linked-data-vocabularies:query-lcsh"]
		)
	}
	setTimeout(cb, 1000)
})
_%>