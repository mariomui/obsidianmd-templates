
# ---Transient Local Citations

<%-    for (const colorName of ["orange" ]) { %>
<%-     let holders = [] %>
<%-     let annotations = it.filter((annotation) => annotation.colorName === colorName) %>
<%-      for (let i = 4,j = 0; i < annotations.length; Math.min(i += 4, annotations.length - 1)) { %>
<%-         let slices = annotations.slice(j,i) %>
<%-         let annot = slices.reduce((chain, slice) => { %>
<%-           chain.text = chain.text + " " + slice.text %>
<%-           chain.pageLabel = slice.pageLabel %>
<%-           chain.parentItem = slice.parentItem %>
<%-           chain.queryParamFig = { page: slice.pageLabel, annotation: slice.key } %>
<%-           chain.blockID = slice.blockID %>
<%-           chain.key = slice.key %>
<%-           return chain                %>
<%-         }, {text: "", blockID: "", queryParamFig: {}, key: "", pageLabel: 0, colorName: "orange"}) %>
<%-           holders.push(annot) %>
<%-          j = i + 1 %>
<%-       } %>
<%-       const uniquePageFig = holders.reduce((chain, holder) => { %>
<%-          const pageLabel = holder.pageLabel; %>
<%-          chain[pageLabel] = true; %>
<%-          return chain; %>
<%-       },{}) %>
<%-       for (let key in uniquePageFig) { %>
<%-          const annots = holders.filter((holder) => holder.pageLabel === key)         %>
<%-          const allText = annots.reduce((chain, holder) => { chain += holder.text; return chain},"") %>
## <%-= `p.${key}` %>

<%-           for (let annot of annots) { %>
<%-~            include("orange", annot) %>
<%-           } %>
<%       } %>
<%-     } %>
<%-   for (const colorName of ["green", "yellow","red","blue" ]) { %>
<%-     let annotations = it.filter((annotation) => annotation.colorName === colorName) %>
<%-     if (annotations.length > 0) { %>
<%-       if (colorName === "green") { %>
<%-       } %>
<%-       if (colorName === "yellow") { %>
<%-       } %>
<%-       for (let annot of annotations) { %>
<%-         const annotTextLength = annot?.text?.length || Infinity %>
<%-         const displayLength = Math.min(45, annotTextLength) %>
<%-         const lcTitle = annot?.text?.substring(0,displayLength) || ""; %>
<%-         const _lcTitle = lcTitle?.split("	")?.filter(Boolean).join(" ") %> 
<%-         const pageLabel = annot.pageLabel ?? ""; %>
<%-         const _lcColor = annot.imgEmbed ? "image" : colorName.substring(0,3) %>
<%-         const _lcParaphrase = _lcTitle || annot.comment || ( annot.docItem.citekey + "-" + annot.imgLink.match(/[A-Za-z0-9]+\.png/) ); %>

## LC--<%= _lcColor %>-Page-<%= pageLabel?.padStart(4,"0") + "--" + (_lcParaphrase) %>

<%~         include("annotation", annot) %>
<%        } %>
<%-     } %>
<%-   } %>
