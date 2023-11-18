<% for (const annotation of it) { %>

### <%= annotation?.dateAdded?.split[" "](0) %>-Page-<%= annotation?.pageLabel + "-" + annotation?.blockID + " " + annotation?.text?.substring(0,30)%>

<%~ include("annotation", annotation) %>
<% } %>
