---
CREATION_DATE: <% tp.date.now("YYYY-MM-DD") %>
DEPENDENCIES:
  - "[[¡-transforming-library-of-congress-heading-into-tag-form,vis-Noteshippo|aka-MUID-2252]]"
DOC_VERSION: v0.0.0
MUID: 
PROJECT_PARENT: 
TEMPLATE_SOURCE: "[[macro-for-prompted-lcsh-specced-note-template,nb.-MUID-142,nb.-v0.0.10]]"
TEMPLATE_VERSION: v0.0.10
tags:
  - _misc/_wip
---
<%*
let lcsh = await tp.system.prompt("What's the lcsh?");
_%>

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

* ! If the [[_lcsh]] requires deprecation, suffix the [[obsolete-vernacular-symbol,uti.-≠,bt.-Noteshippo-pan-level-flag,]] symbol. Do not delete.
	* 🔗 [[suffix-comma-and-≠-to-heading-frontmatter-property-value-to-track-obsoleted-vernacular-in-realtime,nb.-library-of-congress-headings,prima-facie]]
* & [[,aka-lcsh-specced-note]] assigned with "<% lcsh %>" denote ...
	* 
	- 🗃🧮🔗 *broader*: `= list(this.broader)`
	- 🗃🧮🔗 *narrower*: `= list(this.narrower)`
### 11÷Reference

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]].
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`

# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`

* [[##10÷About|10÷About]]
* @ LCSH
	* [[<% lcsh %>]]

---

# ---Transient Jobs

![[interim--~viewfn-for-sluicing-out-embedded-query-into-a-job-queue,nb.-MUID-1934#=|?t=nlk&search_term=[heading: "<% lcsh %>"]]

# ---Transient Local Resources

## LR--query--files having heading with <% lcsh %>

```query
[heading: "<% lcsh %>"]
```

# ---Transient

<%*/** Transient Template Doc Log
[[transient-doc-log-endpoint,bt.-Noteshippo-heading-api,]]
* v0.0.9
	* Fix 10-About link within public api so that it is relative.
	* Add this.narrower and this.broader into About api to help identify whether or not the lcsh is useful in classification.
* v0.0.8 *2025-05-03*
	* Update private header endpoints
	* Add dependencies
	* add DOC_VERSION property field
* v0.0.7 *2025-04-28*
	* Add MUID-142 to macro title
	* Add a little note telling future me to obsolete the vernacular by suffix so that the [[≈.~view-all-lcsh-headings]] can group up the like-minded headings together.
* v0.0.5 *2025-03-25*
	* remove filebn from About because we already know. Also use lcsh specced note to define this spec.
* v0.0.4 *2025-03-22*
	* Upgrade basefp to v0.0.6
	* Meta wraps about and reference api
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
_%
