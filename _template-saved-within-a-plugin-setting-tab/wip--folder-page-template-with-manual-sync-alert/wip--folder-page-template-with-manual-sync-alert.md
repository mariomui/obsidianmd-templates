---
aliases:
  - __README__{{FOLDER_PATH}}
  - "{{FOLDER_PATH}}"
tags:
  - _noteshippo/v1/structural-note
TEMPLATE_SOURCE: "[[wip--folder-page-template-with-manual-sync-alert]]"
TEMPLATE_VERSION: v0.0.0
---

# -

## About

Make sure that the folder page template is synced correctly so i dont have data drift

# =

> [!warning] This note is not yet ready to be used


# ---Transient 010 Jobs

![[~viewfn-sluicing-out-waypoint-like-unprocessed-links-MUID-1643#=|&t=nlk?search_term=---Transient Local Waypoints]]

# ---Transient Local Waypoints

* ! Waypoint cannot be synced with hard coded folder page here

# ---Transient

- [ ] rework the codelet to apply for folder page plugin ➕ 2024-01-16
```
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