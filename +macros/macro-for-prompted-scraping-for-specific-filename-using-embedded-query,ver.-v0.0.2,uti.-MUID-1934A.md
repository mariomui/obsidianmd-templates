<%* 
let filename = await tp.system.prompt("What's the filename to scrape?");
_%>
# ---Transient Jobs

![[~viewfn-for-sluicing-out-embedded-query-into-a-job-queue,nb.-MUID-1934A#=|?t=nlk&search_term=file: <% filename %>]]

# ---Transient Local Resources

## LR--query--filenames containing <% filename %>

```query
file: <% filename %>
```


<%* /**
* LOG
* v0.0.2
	* Added prompted filename.
- v0.0.1
	- Add a new line after Jobs for clarity
- v0.0.0
**/ _%>