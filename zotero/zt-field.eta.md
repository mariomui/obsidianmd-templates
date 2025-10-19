title: "<%= it.title %>"
citekey: "<%= it.citekey %>"
authors: <%- it.authors.forEach(author => { %>
  - <%= author -%> 
<% }) %>
itemType: "<%= it.itemType %>"
manuscriptType: "<%= it?.manuscriptType %>"
abstract: "<%= it?.abstractNote %>"
numPages: "<%= it.numPages || it.pages %>"
isbn: "<%= it?.ISBN_ %>"
DOI: "<%= it?.DOI %>"
publisher: "<%= it.publisher %>"
publicationTitle: "<%= it.publicationTitle %>"
volume: "<%= it.volume %>"
issue: "<%= it.issue %>"
extra: <%- it.extra.forEach(ex => { %>
<%=  ex.toLowerCase() %>
<% }) -%>