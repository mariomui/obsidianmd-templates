<%  if ( ["green", "yellow","red","blue" ].includes(it.colorName) ) { %>
<%-   if (it.colorName === "yellow") { %> 
[!EXAMPLE] %%FAKE TITLE HERE%% 
<%    } %>
<%-   if (it.colorName === "green") { %>
[!TIP] %%FAKE TITLE HERE%%
<% } %>
<%-    if (it.colorName === "red") { %>
[!DANGER] %%FAKE TITLE HERE%%
<%     } %>
<%-= (typeof it?.dateAdded?.split[" "] === "function") ? it?.dateAdded?.split[" "](0) : "" %>
<% if (it.imgEmbed) { %>
- <%= it.imgEmbed %>
<% } %>
<%-= ""%>**file**: <%= it.docItem?.citekey %>
<% if (it.comment) { %>
- <% if (it.comment.startsWith('todo ')) { %>[ ] **<%= it?.comment?.substring(5) %>:**<% } else { %>**<%= it.comment %>:**<% } %>  
  - <%= it.text %> [p. <%= it.pageLabel %>](zotero://open-pdf/library/items/<%= it.parentItem %>?page=<%= it.pageLabel %>&annotation=<%= it.key %>) <% if (it.tags && it.tags.length > 0) { %> <% = it.tags.map(tag => '#' + tag.name).join(", ") %><% } %>  
<% } else if (it.text) { %>
<%= it.text %> [p. <%= it.pageLabel %>](zotero://open-pdf/library/items/<%= it.parentItem %>?page=<%= it.pageLabel %>&annotation=<%= it.key %>) <% if (it.tags && it.tags.length > 0) { %> <% = it.tags.map(tag => '#' + tag.name).join(", ") %><% } %>  
<% } %>
<cite><%= it.docItem?.title %>, <%= it.docItem?.series %> by <%= it.docItem?.authorsShort %>, <%= it.docItem?.date %> </cite>
<% } %>


