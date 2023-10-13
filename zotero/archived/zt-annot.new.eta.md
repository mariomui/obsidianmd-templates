### <%= it.text.substr(0, (it.text.length / 2)) %>

\n
[!note] Page <%= it.pageLabel %>
\n
<%= it.imgEmbed %>
<%= it.text %>

<% if (it.comment) { %>
---

<%= it.comment %>
<% } %>
