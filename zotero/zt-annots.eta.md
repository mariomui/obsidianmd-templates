
# ---Transient Local Citations

<% for (const colorName of ["green", "yellow","red","blue" ]) { %><% let annotations = it.filter(annotation => annotation.colorName === colorName) %><% if (annotations.length > 0) { %> <% if (colorName === "green") { %><% } %><% if (colorName === "yellow") { %><% } %><% for (const annot of annotations) { %>

## LR--<%=colorName?.substring(0,3)%>-citation--Page-<%= annot.pageLabel + "-" + (annot?.text?.substring(0,30) || annot.comment)%>

<%~ include("annotation", annot) %>
<% } %> <% } %> <% } %>
