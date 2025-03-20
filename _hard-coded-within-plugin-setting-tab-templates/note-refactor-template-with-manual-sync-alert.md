---
CREATION_DATE: "{{date:YYYY-MM-DD}}"
MUID:
TEMPLATE_VERSION: v1.0.9_note-refactor-template
UMID: 
tags:
  - _misc/_wip
---

# -

## 00-Meta

![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|nlk]]

```dataview
task where file.name = this.file.name and !completed
```

```dataview
task where file.name = this.file.name and completed
```

## 10-About

### 11-Reference

![[~view-for-referencing-current-jumpid#=|nlk]]

* †

## 20-Inlink

# =

**base_filepath-v0.0.2**: *`= this.file.path`* doc-`= this.DOC_VERSION` / ids: `= this.MUID`,`= this.UMID` / lcsh: `= this.heading` / updated on: `= dateformat(this.file.mday, "yyyy-LL-dd")` / file-size: `= round(this.file.size/1024,2)` KB

{{new_note_content}}

---

# ---Transient

# ---Startup Code

This note is tied to [[note-refactor-template-with-manual-sync-alert]]

> [!info] Place all meta data below this heading.
> Because Note Refactor lies outside of the Templater ecosystem, the normal commenting out using templater code does not work.
> Note Refactor does not have a commenting out system in its templating engine.

See [[callout-feature,vis-ObsidianMD-app,]] for help with which callouts to use to help aid this note.

This [[Library-datum-spec,vis-Noteshippo-taxonomy,]] belongs to  list-of-note-templates,util-Templater-plugin,ad-finem-Note-Taking designed to template extracted content.

```dataviewjs
//toolboxes
const { workspace, vault, plugins, metadataCache } = this.app;
const { default: obs } =
  this.app.plugins.plugins["templater-obsidian"].templater
    .current_functions_object.obsidian;
const nro = plugins.plugins["note-refactor-obsidian"];

// # perms
const { refactoredNoteTemplate: note_template } = nro.settings;




// # Bootstrap
this.app.workspace.onLayoutReady(main.bind(this));

function main() {
  const active = workspace.getActiveFile();
  const producerVf = vault.getAbstractFileByPath(
    this.currentFilePath
  );
  const {frontmatter} = metadataCache.getFileCache(producerVf)
  const TEMPLATE_VERSION = frontmatter?.TEMPLATE_VERSION || "";
  
  const split_mark = "# ---Startup Code";
  const cont = this.container;
  
  const v = workspace
    .getActiveLeafOfViewType(
    obs.MarkdownView
  );
  
  // # Business 
  
  // ## - 
  const [template] = v.data.split(split_mark);
  const cleanedTemplate = clean(template);
  const cleanedNroTemplate = clean(note_template);
  const isSame = cleanedTemplate === cleanedNroTemplate;
  // ### derived sync status  
  const sync_status = isSame ? "Synced" : "Unsynced";
  
  // ## messages
  // ### message components
  const secondary_status_msg = [
    template.length, note_template.length
  ].join(" ");
  const main_status_msg = [
    active.name, "is", sync_status
  ].join(" ");
  // ### status message based on sync status
  const status = [
    main_status_msg, 
    secondary_status_msg
  ].join("\n");

  const el = this.container.createEl("div", {
    text: status,
    attr: {
      style:
        "display: none;\
text-align: center;\
padding: .5em 1em;\
background-color: rgba(\
var(--color-red-rgb), .8);\
",
    },
  });

  // # UI
  const bel = new obs.ButtonComponent(this.container)
    .setButtonText("Re-check template drift " + TEMPLATE_VERSION)
    .onClick(() => showNotice(el));

  bel.buttonEl.style.background = !isSame
    ? "var(--color-red)"
    : "var(--color-blue)";

  const color = isSame ? "var(--color-blue)" : "lightred";
  el.style.background = color;
  showNotice(el);
}

// # Utility
function clean(file_content) {
  return file_content
    .trim()
    .replaceAll(" ", "")
    .replaceAll("\n", "");
}

function showNotice(el) {
  el.style.display = "block";
  new obs.Notice(el, 2000);
}
```
☝Click button to see if note refactor template settings are okay

>[!warning] Do not Remove the Startup Header!
>The header [[#---Startup Code]] is intrinsic to how the file is extracted. Anything blow that anchor header is ignored in the sync check.

>[!note]
>There is a codelet to sync the content inside of  [[#---Startup Code]] with the content in the settings tab of the [[note-refactor-plugin,bt.-ObsidianMD-app,]].

> [!warning] Do not use this template with Templater plugin directly. It only serves as an external backup to the internal settings specified in Note Refactor.
