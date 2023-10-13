---
MUID: <% await app.insertIncrementalId('MUID') %>
tag: [_meta/a-tag-page]
TEMPLATE_VERSION: v1.0.8_tag-page
---
# -

## About

This template is not connected to  [[tag-wrangler-plugin,b.t.-ObsidianMD,]]. Tag wrangler offers no integrated way to use this [[templater-plugin,b.t.-ObsidianMD-app,]] when a new [[Tag-page,util-Tag-Wrangler,]] is created.

 > [!warn] It seems like this template is out of date, and is only used in a handful of older tag-pages.

- [ ] Document exactly what is going on with this tag page. #_todo/to-process/on-a-dataviewjs-codelet/regarding-reasons-for-its-deprecation
  - Why is the [[#Dashboard For Current Tag Only Notes]] not being used?
    - The dashboard is now  [[Partial-dataview,vis-Noteshippo]] powered.
      - See [[~view-for-exact-tag-file-listing#-]] for details.

* ⚙ The tag ( `= this.file.aliases[0] ` ) will be for:
    * †
* 🔎  *Examples*:
    * †
    
Because this 

# =


## Dashboard For Current Tag Only Notes

See [[external-guide-to-creating-dataview-plugin-powered-codelets#Ways to Create a Cta Button]]

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

[[interim_tag-page-template-commit-history]]