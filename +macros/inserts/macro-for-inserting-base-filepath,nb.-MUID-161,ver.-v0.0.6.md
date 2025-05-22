**base_filepath-v0.0.6**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT` / lcsh: `= link(this.heading)`

<%_* /**
* v
	* Updating filename with MUID
	* Update nb version to ver
* v0.0.6 *2025-03-17*
	* create a link from the lcsh. This way i can create the lcsh after [[linked-data-vocabulary-plugin,bt.-Obsidianmd-app,]] is finished populating the frontmatter
* v0.0.5 *2025-03-15*
	* replace this.umid with this.project_parent
	* display the full path as wikilink
* v0.0.4 *2025-03-14*
	* When the filename is a folder note, display it as a wikilink instead of plain text.
* v0.0.3 *2025-02-13*
  * retrieving the date and the filesize creates a lag unlike anything i've ever seen. Remove both from inline dql.
* v0.0.2 *2025-01-23*
  * Upper Part
    * *`= this.file.path`*
  * Lower Part (deliminated by backslash)
    * doc-`= this.DOC_VERSION`
    * ids:
      * `= this.MUID`/
      * `= this.UMID`/
    * lcsh:
      * `= this.heading`/
    * updated on:
      * `= dateformat(this.file.mday, "yyyy-LL-dd")`/
    * file-size:
      * `= round(this.file.size/1024,2)` KB
**/_%>