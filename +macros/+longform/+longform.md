---
aliases:
  - __README__Y_templates/_macros/+longform
  - Y_templates/_macros/+longform
tags:
  - _meta
---

# -

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[π-Lists-all-inlinks,nb.-MUID-128,nb.-0.0.5|experiment note]]. 
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`


# =

* [[macro-for-novel-outline-template,cf.-Kanzi]]
  * 💁 This outline is powered by the thinking from:
    * [[¡-using-Hubbardian-story-idea-creation-process,cf.-Writers-of-the-future,vis-Writeshippo]] 
    * [[†-Writers-of-the-Future-Online-Workshop-Writers-&-Illustrators-of-the-Future-https-www-writersofthefuture-com-lessons-essay-magic-out-of-a-hat]] 
    * [[seven-point-structure-plotting,cf.-Dan-Wells,vis-Writing,]]
* [[macro-for-april-automatic-timelines-required-fields-only]]
* [[wip--macro-for-canoe-template-for-character-creation]]
* @ Character Creation
	* [[ᛏ--Amica]]
		* [[macro-for-abacus-seeds]]
		* [[macro-view-for-calculating-fcdate-fcend-diff,nb.-v1.0.9]]
* @ Bullet Guides
	* # Character Creation
* @ Time Line Event Creation
	* [[macro-to-example-inline-dql-that-calculates-two-fc-dates-with-abacus]]
* @ One Off 
	* Used primarily for [[∫-The-Emotional-Wound-Thesaurus-A-Writer's-Guide-to-Psychological-Trauma-—-Becca-Puglisi-Angela-Ackerman]]
		* [[macro-for-emotional-wound-citums]]
			* ? This is a little outdated
		* [[macro-for-emotional-wound-bullet-list-template]]
	* # Tewaz Story
		* ! 🛏 TODO Modify macros to scrape the rune (tewaz) dynamically so it can apply to more story types
		* [[macro-for-tewaz-broader-query]]
		* [[macro-for-tewaz-chapter-template]]
		* [[macro-for-tewaz-metadata]]
* @ Candidates
	* ! 🛏 TODO Phase plan these attributes by priority and foundational nature
		* [[wip--macro-for-character-sheet-template,vis-Writing,cf.-Luke]]
			* I don't quite use this as i believe it's easier to build just in time.
			* It makes more sense to mark these characteristics by scheduled best build moment, whether which attribute group should be build first. 


# ---Transient 010 Jobs

![[~viewfn-sluicing-out-waypoint-like-unprocessed-links,nb.-MUID-1643#=|&t=nlk?search_term=---Transient Local Waypoints]]

# ---Transient Local Waypoints

%% Begin Waypoint %%
- [[macro-for-abacus-seeds]]
- [[macro-for-april-automatic-timelines-required-fields-only]]
- [[macro-for-emotional-wound-bullet-list-template]]
- [[macro-for-emotional-wound-citums]]
- [[macro-for-novel-outline-template,cf.-Kanzi]]
- [[macro-for-tewaz-broader-query]]
- [[macro-for-tewaz-chapter-template]]
- [[macro-for-tewaz-metadata]]
- [[macro-to-example-inline-dql-that-calculates-two-fc-dates-with-abacus]]
- [[macro-view-for-calculating-fcdate-fcend-diff,nb.-v1.0.9]]
- [[wip--macro-for-canoe-template-for-character-creation]]
- [[wip--macro-for-character-sheet-template,vis-Writing,cf.-Luke]]

%% End Waypoint %%

# ---Transient
