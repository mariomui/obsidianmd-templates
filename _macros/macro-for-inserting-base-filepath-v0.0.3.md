**base_filepath-v0.0.3**: *`= this.file.path`* doc-`= this.DOC_VERSION` / ids: `= this.MUID`,`= this.UMID` / lcsh: `= this.heading`

<%* /**
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
