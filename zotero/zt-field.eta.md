title: "<%= it.title %>"
citekey: "<%= it.citekey %>"
authors: <%- it.authors.forEach(author => { %>
  - <%= author -%> 
<% }) %>
itemType: "<%= it.itemType %>"
numPages: "<%= it.numPages || it.pages %>"
extra: "<%= [] %>"
isbn: "<%= it?.ISBN_ %>"
DOI: "<%= it?.DOI %>"
publisher: "<%= it.publisher %>"
publicationTitle: "<%= it.publicationTitle %>"
volume: "<%= it.volume %>"
issue: "<%= it.issue %>"
extra: <%- it.extra.forEach(ex => { %>
<%=  ex.toLowerCase() %>
<% }) -%>