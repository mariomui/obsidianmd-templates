<%*
let enumKRL
(function enumKRL(enumKRL) {
	enumKRL[enumKRL["TODO"] = 0] = "TODO";
	enumKRL[enumKRL["DONE"] = 1] = "DONE";
})( enumKRL || (enumKRL = {}) )
// enums are super complicated for no reason. i'm never doing this again.
// I understand why the inner expression is evaluated. But why is the output of the inner expression transferred as the evaluated value? An assignment statement usually has the value of undefined.

const INSERTFIG = {
	[enumKRL.TODO]: "* ! 🛏 TODO",
	[enumKRL.DONE]: "* $ ✅ DONE"
}
tp.app.workspace.onLayoutReady( bootup.bind(this) );

function bootup() {
	const boundedGenMain = genMain.bind(this);
	(boundedGenMain)()
}


async function genMain() {
	const choice = await tp.system.suggester(
		(item) => item, [ enumKRL[enumKRL.TODO], enumKRL[enumKRL.DONE] ]
	);
	console.log({choice})

	await tp.file.cursor_append(
		`${INSERTFIG[ enumKRL[choice] ]}`
	);
}
_%>

