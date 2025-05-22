---
CREATION_DATE: <% await tp.file.creation_date("YYYY-MM-DD")%>
DOC_VERSION: v0.0.0
MUID: <% await app.insertIncrementalId('MUID') %>
PROJECT_END_DATE: 
PROJECT_PARENT: "[[<% await tp.file.title %>]]"
TEMPLATE_SOURCE: "[[10--project-note-template,nb.-MUID-192]]"
TEMPLATE_VERSION: v1.0.13
aliases: 
tags:
  - _misc/_wip
---

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

> [!info] Hover over me [[~view-for-recent-reference-link-to-note-title-transform,nb.-MUID-115]] and copy normalized note title.

- has been undergoing for,
	- $ 🧮 `= (date(today) - (this.CREATION_DATE)).weeks` weeks 
- will be due in
	- ! 🧮 `= round((this.PROJECT_END_DATE - (this.CREATION_DATE)).weeks)` weeks 

<%* 
const title = await tp.file.title;

new tp.obsidian.Notice("Please add an end date. Default is next year.");

// Mutate end date to be 1 year end.
tp.hooks.on_all_templates_executed(async () => { 
	const tfile = tp.file.find_tfile(
		tp.file.path(true)
	);
	const fv = tp.app.workspace.getActiveFileView()
	const fm = fv.metadataEditor.serialize()
	fm["PROJECT_END_DATE"] = tp.date.now("YYYY-MM-DD", "P1Y");
	await fv.metadataEditor.synchronize(fm);
	await fv.save();
	fv.refreshEditor();
});
-%>
### 11÷Reference

> [!info] Hover over [[~view-for-referencing-current-jumpid]] for jumpid alias

* †

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`



# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`



# ---Transient Jobs

![[interim--~viewfn-for-sluicing-out-embedded-query-into-a-job-queue,nb.-MUID-1934#=|?t=nlk&search_term=[PROJECT_PARENT: <% title %>]]

# ---Transient Local Resources

## LR--query--files having heading with <% title %>

```query
[PROJECT_PARENT: <% title %>]
```




# ---Transient

<%* /** Journal
* *2025-05-11* 
	* 🐛 When applying template to a new note, the expected behavior is that the [[project_end_date,bt.-Noteshippo-frontmatter-property-name,nb.-project-template,]] is populated with the date value 365 days later. The actual behavior and value is blank.
		* 💫 🔑 [[≈-project-note-template]]
**/_%>
<%_* /**
* v
	* 
* v1.0.13 *2025-04-10*
	* Add collapsible meta ep
- v1.0.12 *2025-03-20*
	- add 20 inlink sub endpoint to meta api
- v1.0.11
	- PROJEcT PaTh field value must be a link and the title itself
	- automate the frontmatter link scrape
	- add project end date
	- update basefp to v0.0.6
	- remove commit log header
	- test out tp.file.title in frontmatter
	- remove UMID code
- v1.0.9
	- add the term project note to UMID
- v1.0.8
  - add commonly used macro that shows filepath and doc version
* v1.07
  * change the name to show that this template is a template that has UMID In it, meant for big projects.
* v1.0.6 
  * Add template source into metadata
  * Revert the DOC_VERSION to v0.0.0
  * Update filename to filepath in the public api
  * Conform tasks to be under the Meta h2
  * Remove the reading time partial dataview
  * Update the note title transform ~dataview to use callouts
  * Update the reference jumpid ~dataview to use callouts
* v1.0.5 Add a new line after jumpid codelet for better contrast on reflink

**/ -%>
