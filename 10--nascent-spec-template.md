---
CREATION_DATE: <% tp.file.creation_date("YYYY-MM-DD") %>
DEPENDENCIES:
  - "[[,aka-MUID-152]]"
  - "[[,aka-MUID-161]]"
DOC_VERSION: v0.0.0
MUID: 
PROJECT_PARENT: 
TEMPLATE_SOURCE: "[[10--nascent-spec-template]]"
TEMPLATE_VERSION: v1.0.14
tags:
  - _misc/_wip
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

### 11÷Reference

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> >`= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`



# =

**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`






# ---Transient

<%* /** ---Transient Commit Log 
By order of recency
* v1.0.14 *2025-05-15*
	* Fix doc version not conforming to semver standard
* v1.0.13 *2025-05-06*
	* Update private header endpoints
* v1.0.12 *2025-04-01*
	* Replace with collapsible meta api endpoint
* v1.0.11 *2025-03-17*
	* alphaSort frontmatter
	* add project parent
	* place about and reference inside of 00 meta
	* Update base fp to v0.0.6
* v1.0.10 *2025-02-20*
	* update basefilepath
	* update all inlink endpint
* v1.0.9 *2025-01-23*
	* Add v0.0.4 of [[macro-for-insert-of-all-inlink-endpoint,uti.-inline-dql,cf.-MUID-128,nb.-MUID-150,ver.-0.0.5]]
	* Add v0.0.2 of [[macro-for-inserting-base-filepath,nb.-MUID-161,ver.-v0.0.6]]
	* Fully label The transient commit log to show it applies to macros and templates as well
* v1.0.8 *2025-01-06*
	* Add a creationdate to frontm
* v1.0.7
	* Replace file_basename with the base_filepath in order to have the full folder path
* v1.0.6
	* Add the Dewey Decimal prefix to the private API so that when the notetaker alphabetically sort the headings, they retain their ordinal value. 
* v1.0.5
	* Replace file_basename with one that include UMID and lcsh heading
* v1.0.4
  * unitalicize the doc version in the public api response
* v1.0.3 *2024-06-09*
  * Conform included file basename naming standards using pattern found in [[ø--macro-for-commonly-used-file-and-filepaths-inserts]]
* v1.0.2 *2024-05-28*
  * Replace commonly used base filename with one that includes the doc version
* v1.0.1
  * Add wip tag
* v1.0.0
  * add only the basic set of fields for nascent. Its purpose is to provide a template for notes that do not need a MUID such as notes affixed with [[interim-symbol,uti.-self,bt.-Noteshippo-title-level-flag,]]
**/ -%>