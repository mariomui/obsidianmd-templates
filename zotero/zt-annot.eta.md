<% if (it.colorName === "yellow") { %> 
[!EXAMPLE] %%FAKE TITLE HERE%% 
<% } %> 
<% if (it.colorName === "green") { %>
[!TIP] %%FAKE TITLE HERE%%
<% } %>
<% if (it.colorName === "red") { %>
[!DANGER] %%FAKE TITLE HERE%% 
<% } %>  <%= it.dateAdded.split(" ")[0] %>
<% if (it.imgEmbed) { %>
- <%= it.imgEmbed %>
<% } %>
<% if (it.comment) { %>
- <% if (it.comment.startsWith('todo ')) { %>[ ] **<%= it.comment.substring(5) %>:**<% } else { %>**<%= it.comment %>:**<% } %>  
	- ==<%= it.text %>== [p. <%= it.pageLabel %>](zotero://open-pdf/library/items/<%= it.parentItem %>?page=<%= it.pageLabel %>&annotation=<%= it.key %>) <% if (it.tags && it.tags.length > 0) { %> <% = it.tags.map(tag => '#' + tag.name).join(", ") %><% } %>  
<% } else if (it.text) { %>
- ==<%= it.text %>== [p. <%= it.pageLabel %>](zotero://open-pdf/library/items/<%= it.parentItem %>?page=<%= it.pageLabel %>&annotation=<%= it.key %>) <% if (it.tags && it.tags.length > 0) { %> <% = it.tags.map(tag => '#' + tag.name).join(", ") %><% } %>  
<% } %>