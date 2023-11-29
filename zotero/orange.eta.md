<%-   const text = it.text %>
<%-   const parentItem = it.parentItem %>
<%-   const pageLabel = it.pageLabel %>
<%-   const queryString = (new URLSearchParams(it.queryParamFig)).toString() %>
<%-   const zoteroDomain = "zotero://open-pdf/library/items" %>
* <%-=`[${text}](${zoteroDomain}/${it.parentItem}?${queryString})` -%>
