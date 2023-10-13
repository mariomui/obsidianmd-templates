<% for (const colorName of ["green", "yellow","red" ]) { %> <% let annotations = it.filter(annotation => annotation.colorName === colorName) %> <% if (annotations.length > 0) { %> <% if (colorName === "green") { %> 
## ⏰ Dive Deep Later List <% } %> <% if (colorName === "yellow") { %>
# ---Transient Local Citations <% } %>
<% for (const annot of annotations) { %>
## LR--citation--Page-<%= annot.pageLabel + "-" + annot.blockID + " " + annot.text.substring(0,30)%>

<%~ include("annotation", annot) %>
<% } %> <% } %> <% } %>