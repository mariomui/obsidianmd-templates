---
CREATION_DATE: <% tp.date.now("YYYY-MM-DD") %>
DEPENDENCIES:
  - "[[,aka-dependencies,cf.-MUID-142]]"
DOC_VERSION: v0.0.0
MUID: 
PROJECT_PARENT: 
TEMPLATE_SOURCE: "[[macro-for-prompted-lcsh-specced-note-template,nb.-MUID-142]]"
TEMPLATE_VERSION: v0.0.13
tags:
  - _misc/_wip
---
<%*
let lcsh = await tp.system.prompt("What's the lcsh?");
_%>

# -

## 00-Meta

> [!info]- Progress Bar v0.0.3
> > ![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|olk]]
> ```dataview
> task where file.name = this.file.name and !completed
> ```
> >
> ```dataview
> task where file.name = this.file.name and completed
> ```

### 10÷About

* ! If the [[_lcsh]] requires deprecation, suffix the [[obsolete-vernacular-symbol,uti.-≠,bt.-Noteshippo-pan-level-flag,]] symbol.
* & [[,aka-lcsh-specced-note]] assigned with "[[<% lcsh %>]]",
	* 📃✨
	* 🔢  *as of <% tp.date.now("YYYY-MM-DD") %>*:
	* 🗃🧮🔗 *locuri*: `= this.uri`
	* 🗃🧮🔗 *broader*: `= map(this.broader, (x) => link(x))`
	* 🗃🧮🔗 *narrower*: `= map(this.narrower, (x) => link(x))`
	* 🗃🧮🔗 `= link(this.file.frontmatter.heading)`

---
### 11÷Reference

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-design-codelet-that-lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]].
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`

# =

**base_filepath-v0.0.9**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT`,alias: *`= this.aliases`*,nb: *`=this.NOTA_BENE`* , authors: *`= this.authors`* / lcsh: `= link(this.heading)`

* [[##10÷About|10÷About--nlk]]
	* ![[##10÷About|10÷About--nlk]]

---

# ---Transient Jobs

![[~viewfn-for-sluicing-out-embedded-query-into-a-job-queue,nb.-MUID-1934#=|?t=nlk&search_term=[heading: "<% lcsh %>"]]

# ---Transient Local Resources

## LR--query--files having heading with <% lcsh %>

```query
[heading: "<% lcsh %>"]
```

# ---Transient

<%* /** README
	* ! DO NOT VERSION IN TITLE. THIS IS A MACRO TEMPLATE TYPE

**/_%>
<%* /** Transient Template Doc Log
[[transient-doc-log-endpoint,bt.-Noteshippo-heading-api,]]
- v0.0.14
	- update u/[[macro-for-inserting-base-filepath,nb.-MUID-161,ver.-v0.0.9]] v0.0.7-v0.0.9
* v0.0.13 
	* add link to heading of lcsh in meta
* v0.0.12 *2025-05-27*
	* apply [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]] * -> v0.0.3
	* Reserve the public api for thought space. Relegate the lcsh metadata to the [[about-header-endpoint,bt.-Noteshippo-heading-api,nb.-common-type]]
	* Add [[frequency-symbol,uti.-1234-emoji,bt.-Noteshipp-content-level-affix,]] to template; it stands for frequency of current lcsh applied to books as of [DATE]
	* Bump template version
	* ! Remove versioning from title because macro-templates follow template titling rules
	* A
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
_%>