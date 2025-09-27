---
CREATION_DATE: "{{date:YYYY-MM-DD}}"
MUID: 
TEMPLATE_VERSION: v1.0.10_note-refactor-template
PROJECT_PARENT: 
tags:
  - _misc/_wip
---

# -

## 00-Meta

> [!info]- Progress Bar v0.0.3
> > ![[~view-for-local-tasks-using-a-progress-bar,nb.-MUID-698#=|olk]]
> ```dataview
> task where file.name = this.file.name and !completed
> ```
> >
> ```dataview
> task where file.name = this.file.name and completed
> ```

### 10÷About

### 11÷Reference

* †

## 20-Inlink

> [!abstract]- %%  %% Automated List of Reference Inlinks (v0.0.5)
> * ℹ Commit/design logs are located in this [[,aka-MUID-150|experiment note]].
> > `= join( map( sort( map( filter(this.file.inlinks, (link) => meta(link).path != this.file.path), (x) => [ split(meta(x).path, "/")[length(split(meta(x).path, "/")) - 1], x ] ) ), (b) => "• " + choice( length(b[0]) > 28, link( b[1], truncate( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", ""), length( regexreplace(b[0], "(-of|of|the|-the|-for|-that|https-|ee)", "") ) * 0.75 ) ), link(b[1], regexreplace(b[0], "\.md$", "")) ) ), "<br>" )`

# =

**base_filepath-v0.0.9**: `= choice( contains(this.file.folder, this.file.name), link(this.file.path), join(["*",this.file.path,"*"], ""))` doc-`= this.DOC_VERSION` / ids: `= this.MUID`,PP:`= this.PROJECT_PARENT`,alias: *`= this.aliases`*,nb: *`=this.NOTA_BENE`* , authors: *`= this.authors`* / lcsh: `= link(this.heading)`

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
>There is a codelet to sync the content inside of  [[#---Startup Code]] with the content in the settings tab of the [[note-refactor-obsidian-plugin,bt.-Obsidianmd-app,]].

> [!warning] Do not use this template with Templater plugin directly. It only serves as an external backup to the internal settings specified in Note Refactor.
