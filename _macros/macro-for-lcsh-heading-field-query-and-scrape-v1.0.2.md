<%* 
const term = tp.system.prompt("What's the search term",null, true,false);
_%>

# ---Transient Jobs

![[interim--~viewfn-for-sluicing-out-embedded-query-into-a-job-queue,nb.-MUID-1934#=|?t=nlk&search_term=[heading: <% term %>]]

# ---Transient Local Resources

## LR--query--files having heading with <% term%>

```query
[heading: <% term %>]
```

<%* /**
- v1.0.2
	- use macro to dynamically get the lcsh heading term on execute
- v1.0.1 
  - Default the use of the embedded query macro. By default, it scrapes the heading field tag for the target. Replace all ... with the correct lcsh tag
**/ %>