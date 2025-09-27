- ⚛🏛  

<%_*
let enumKRL
(function enumKRL(enumKRL) {
	enumKRL["VERB"] = "VERB";
	enumKRL["NOUN"] = "NOUN";
	enumKRL["ADJECTIVE"] = "ADJECTIVE";
})( enumKRL || (enumKRL = {}) )

const INSERTFIG = {
	[enumKRL.VERB]: "MUID-3322",
	[enumKRL.NOUN]: "MUID-3065",
	[enumKRL.ADJECTIVE]: "MUID-3231"
}
const MUIDS = Object.values(INSERTFIG).sort();
// MUID-3256 (backlog id) <-- BACKLOG 🎲🐛 Possible bug is that the backlog title changes which creates a [[data-drift,etc]] situation. Unlike notes that have their [[,aka-MUID]] in their titles facilitating a search, programatically, an unindexed search would be nonviable, requiring a unoptimized sequential vault wide search.

tp.app.workspace.onLayoutReady( bootup.bind(this) );

function bootup() {
	const dataviewPlugin = this.app.plugins.plugins["dataview"];
	const dv = dataviewPlugin.api;
	if (!dv) return;
	const effs = getFileDVPkgByPredicate(dv, MUIDS, "MUID")

	
	const boundedGenMain = genMain.bind(this);
	(boundedGenMain)(effs)
}


async function genMain(effs) {

	const keys = Object.keys(INSERTFIG)
	/**
	 * @param callback {(k) => T} where k is the transformed display 
	 * @param keys {any[]} where items in array are the return value. No transformation of the values are allowed.
	**/
	const choice = await tp.system.suggester((key) => key, keys
		// This should be the actual documented code on the site but as of *2025-05-30* it is still not. Original doc [tp.system - Templater](https://silentvoid13.github.io/Templater/internal-functions/internal-modules/system-module.html#examples-2) favors the truncated version where the return value can be mistaken for a tuple.
	);
	const CHOSEN_MUID = INSERTFIG[choice];
	const eff = effs.find((eff) => eff.MUID === CHOSEN_MUID)
	
	await tp.file.cursor_append(
		` [[${eff.file.name}]]`
	);
}


/**
* @return dataview values containing the MUID in question
**/
function getFileDVPkgByPredicate(
	dv, targets, field_name
) {
	const pages = dv.pages().where((p) => {
		return targets.includes(p[field_name])
	})
	return pages.values;
}
_%>
<%* /** README 
- This macro is to aid a commonly used composite affix that indicates the type of grammar primitive of a vocabulary word. 
- 🔗 [[element-heading-symbol,uti.-atom_symbol-emoji,bt.-Noteshippo-CLA,]] + [[interim--class-type-category-symbol,uti.-classical_building-emoji,bt.-Noteshippo-CLA,]]
- 🔗 🐊 Borrows  heavily from [[≈.interim--macro-for-choice-prompted-kanban-root-label-insertion,nb.-MUID-197,ver.-v0.0.1]]
**/_%>

<%* /** Commit Log

* v0.0.1

**/_%>