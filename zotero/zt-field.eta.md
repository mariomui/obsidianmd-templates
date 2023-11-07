title: "<%= it.title %>"
citekey: "<%= it.citekey %>"
authors: <%- it.authors.forEach(author => { %>
  - <%= author -%> 
<% }) %>