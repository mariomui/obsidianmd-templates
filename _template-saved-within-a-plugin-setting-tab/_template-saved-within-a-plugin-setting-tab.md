---
aliases: ["__README___manually-placed"]
TEMPLATE_VERSION: v1.0.0-folder-page
CREATION_DATE: 2023-06-17 
tags: _meta _noteshippo/structural-note
UMID: 
---

# -

[[Templater-plugin-for-obsidianmd-should-only-use-templates-from-a-single-assigned-folder]]

```dataview
task where file.name = this.file.name and !completed
```


## About

- [ ] Does changing a folder page's name require also updating the aliases? #_todo/to-muse/on-noteshippo 

# =

This folder houses all the templates that need to be manually added into the plugin settings;

Due to limitations of the API, I can only check the contents of the template against the plugin only when you visit the page.

# ---Transient

Should the dataview "List of templates hard coded within plugin settings v0.0.0" be colocated into a partial view?

```dataview
TABLE WITHOUT ID file.link as "List of templates hard coded within plugin settings v0.0.0"
WHERE startswith(file.path,this.file.folder)
LIMIT 50
```
