---
MUID: <% await app.insertIncrementalId('MUID') %>
tag:
  - _noteshippo/∑≠--v1-spec/∑≠tag-page
TEMPLATE_VERSION: v1.0.8_tag-page
---
# -

[[obsolete-vernacular-symbol,uti.-≠,bt.-Noteshippo-pan-level-flag,]]
## 10-About

- This template is not connected to  [[tag-wrangler-plugin,bt-ObsidianMD-app,]]. Tag wrangler offers no integrated way to use this [[templater-plugin,bt.-ObsidianMD-app,]] when a new [[Tag-page,uti-Tag-Wrangler,]] is created.

 > [!warn] It seems like this template is out of date, and is only used in a handful of older tag-pages.

- [ ] Document exactly what is going on with this tag page. #_todo/to-process/upon-codelet/regarding-dataviewjs/regarding-reasons-for-its-deprecation
  - Why is the [[#Dashboard For Current Tag Only Notes]] not being used?
    - The dashboard is now  [[Partial-dataview,vis-Noteshippo,]] powered.
      - See [[ƒ--~view-for-exact-tag-file-listing,nb.-v1.0.7,nb.-MUID-105#-]] for details.

* ⚙ The tag ( `= this.file.aliases[0] ` ) will be for:
    * †
* 🔎  *Examples*:
    * †
    

# =

- ! OBSOLETED CONTENT
## Dashboard For Current Tag Only Notes

See [[¬--list-of-code-snippets,by-x,uti.-dataview-plugin-api,vis-Obsidianmd-app#Ways to Create a Cta Button]]

~~~javascript
` // ⚙ Wrap codeblock with single tick to trigger syntax highlights
```dataviewjs

const {default: obs} = this.app.plugins.plugins['templater-obsidian'].templater.current_functions_object.obsidian

if (!this.marioConfig) {
    this.marioConfig = {
        ...this.marioConfig, 
        dvel:dv.el("button", "Refresh"),
        handle: () => new obs.Notice('', 7000)
    }
    this.marioConfig.dvel.addEventListener(
        'click',
        this.marioConfig.handle
    );
    
    const alias = dv.current?.().aliases?.[0];
    if (alias) createDashboard(alias);
} else if (this.marioConfig.dvel && this.marioConfig.handle) {
    this.marioConfig.dvel
        .removeListener(this.marioConfig.handle)

}


function createDashboard(alias = "#_") {
    dv.execute(`
        table join(file.etags,"") as tags
        from ${alias}
        FLATTEN join(
            filter(
                file.etags , 
                (x) => startswith(x,alias)
            )
        ) as maps
        WHERE length(maps) = 0
        sort file.ctime desc
    `)
} 
```

~~~


# ---Transient

[[ø--tag-page-template-commit-history]]

