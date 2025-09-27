
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

### 11÷Reference


## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[,aka-MUID-150|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`

<%* /** Readme
* 🔗 [[meta-endpoint,bt.-Noteshippo-heading-api,]]
**/_%>
<%* /** Commit Log
* v0.0.3 *2025-08-06*
	* Update [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]] v0.0.2 -> v0.0.3
* v0.0.2 *2025-05-07*
	* Test [[interim--macro-for-bumping-version-no-of-callout-progress-bar,cf.-MUID-698,nb.-MUID-182]] on MUID-151.
		* After testing, it is decided that each macro should have their own dedicated updating macro. (after I figure out how to call macros programmatically);
* v0.0.1 *2025-05-01*
	* Apply [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]] ver0.0.1 
	* Add [[about-header-endpoint,bt.-Noteshippo-heading-api,nb.-common-type]] 
	* Add [[reference-endpoint,bt.-Noteshippo-heading-api,]]
	* Apply [[macro-for-inserting-local-page-tasks,nb.-MUID-147,ver.-v0.0.3]]
	* Apply [[macro-for-insert-of-all-inlink-endpoint,uti.-inline-dql,cf.-MUID-128,nb.-MUID-150,ver.-v0.0.5]] v0.0.5
* v0.0.0
**/_%>