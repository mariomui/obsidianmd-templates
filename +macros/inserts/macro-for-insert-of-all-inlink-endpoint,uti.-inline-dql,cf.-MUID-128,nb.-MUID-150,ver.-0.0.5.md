## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`

<%*/** COMMIT LOG.

* v 
	* Add MUID to title.
	* Add version to title.
	* Re-add the need for a commit log per macro even if they do have a experiment note because there are low-level details needing documentation (such as title changes).
* v0.0.5 *2025-02-20*
	* Update to v0.0.5
* v0.0.3 *2025-01-23*
	* Because the experiment note is so coupled to this macro, this commit log is hereby deprecated. See MUID-128 for log details
* v0.0.2 *2025-01-23*
	* Create a sort on inlinks before rendering
**/_%>