<% if (it.colorName == "yellow") { %>  
[!QUESTION] %%FAKE TITLE HERE%%
<% } else { %>  
[!SUCCESS] %%FAKE TITLE HERE%%
<% } %> Page <%= it.pageLabel %>

<%= it.imgEmbed %>
<%= it.text %>

<% if (it.comment) { %>
---
* <%= it.comment %>
<% } %>
\n

