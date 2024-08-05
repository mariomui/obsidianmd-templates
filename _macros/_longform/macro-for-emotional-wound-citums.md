
<%*
const preamble = "## LC--citum"
const mesos = [
  manuMeso(0, "fears"),
  manuMeso(1, "false beliefs"),
  manuMeso(2,"attributes and flaws"),
  manuMeso(3,"needs that are ignored"),
  manuMeso(4,"triggers of trauma"),
  manuMeso(5,"opportunities to heal"),
  manuMeso(6, "behaviors"),
];

(async function genMain() {

  const wound = await genWound() 

  await genWriteMesos(
    mesos,
    preamble,
    capText(wound)
  );
})()

function manuMeso(order = 0, content = "") {
  return {order, content}
}
function capText(text) {
  return text?.toUpperCase() || "";
}
function padNum(num, limit = 2) {
  const p_num = parseFloat(Number(num))
  const numTextLen = String(num).length
  
  if (numTextLen > limit) return num; 
  console.log("do i get here");
  const diff = limit - numTextLen;
  return p_num.toFixed(diff).split(".").reverse().join("")
}
function replaceMiddleWithContent(meso_content) {
  return `list of ${meso_content} stemming from`;
} 
async function genWound() {
  return await tp.system.prompt("What is the emotional wound to insert into citums?", null, true, false)
}
async function genWriteMesos(mesos, preamble, wound) {
  const woundShortName = wound.split(" ").reduce((chain, w) => {
    return chain += (w.substr(0, 2) + ".");
  }, "").split(".").slice(0,3).join(".")

  const genOps = []
  const _mesos = mesos.slice().sort((a,b) => {
    const orderA = a["order"];
    const orderB = b["order"];
    if (orderA < orderB) return -1
    if (orderA > orderB) return 1
    return 0;
  })
  for (let i = 0; i < _mesos.length; i++) {
    const {order, content} = _mesos[i];
    const replacedMeso = replaceMiddleWithContent(content);
    const paddedNum = padNum(order)
    console.log({paddedNum})
    genOps.push(
      await tp.file.cursor_append(
        `${preamble}-${paddedNum}-${woundShortName}--${replacedMeso} ${wound}\n\n`
      )
    )
  }
  return Promise.all(genOps)
}
%>