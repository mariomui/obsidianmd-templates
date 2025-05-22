
<%*
tp.app.workspace.onLayoutReady(boot.bind(this))

function boot() {
	main();
}
function main() {
	tp.hooks.on_all_templates_executed(genFire) 
	
	async function genFire() {
		const testFig = {a: "a", b: "b"}
		const prompt = await tp.system.prompt("prompt");
		const suggester = await tp.system.suggester(Object.keys(testFig), Object.values(testFig), "suggest")
	}
}
%>
















































