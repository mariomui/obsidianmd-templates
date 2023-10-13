<% for (const color of ['#e56eee', '#5fb236', '#f19837', '#2ea8e5', '#ffd400', '#a28ae5', '#ff6666', '#aaaaaa']) { %>
<% let annotations = it.filter(annotation => annotation.color === color) %>
<% if (annotations.length > 0) { %>

<% if (color === '#e56eee') { %>

## ⚡ Hypotheses

<% } %>
<% if (color === '#5fb236') { %>

<!-- ## 💡 Main ideas and conclusions -->
## ⏰ Dive Deep Later List

<% } %>
<% if (color === '#f19837') { %>

## ⚙️ Method

<% } %>
<% if (color === '#2ea8e5') { %>

## ❔ Questions

<% } %>
<% if (color === '#ffd400') { %>

<!-- ## ⭐ Important -->
## ⭐ Highlights

<% } %>
<% if (color === '#a28ae5') { %>

## 🧩 Definitions and concepts

<% } %>
<% if (color === '#ff6666') { %>

## ⛔ Weaknesses and caveats

<% } %>
<% if (color === '#aaaaaa') { %>

## 📣 Survey instruments

<% } %>

<% for (const annotation of annotations) { %>

<%~ include("annotation", annotation) %>

<% } %>
<% } %>
<% } %>
