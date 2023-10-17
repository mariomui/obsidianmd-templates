---
alias:
TEMPLATE_VERSION: v1.0.4_video-note-taking
DOC_VERSION: v0.0.2
CREATION_DATE: 2022-08-05
tag: _wip
UMID:
---

# -

![[~view-for-local-tasks-using-a-progress-bar-MUID-698#=|nlk]]

```dataview
task where file.name = this.file.name and !completed
```

```dataview
task where file.name = this.file.name and completed
```

## About

- [ ] Remove buttons as a dependency from code.
- [ ] Does this deprecate [[~deprecated_button-for-ytranscript]]?

### Reference

- https://www.youtube.com/example
- [[√-LEADERSHIP-LAB-Writing-Beyond-the-Academy-1-23-15-YouTube-https-www-youtube-com-watch-v=aFwVf5a3pZM]] has some code to properly include the Youtube Transcripting Code without running into dataview issues.

# =

## Transcript Control

```dataviewjs
// v1.0.4
const {default: obs} = this.app.plugins.plugins['templater-obsidian'].templater.current_functions_object.obsidian

const {workspace,metadataCache, vault} = this.app;
const {container} = this;
const priority_prefix = "√"

const getCurrentVersion = (ctx) => {
  const source_path = ctx.currentFilePath
  const sourcedAbstractFile = vault
    .getAbstractFileByPath(source_path);

  const {frontmatter} = metadataCache
    .getFileCache(sourcedAbstractFile);
  return parseFrontmatter(frontmatter, "VERSION");
}
const VERSION = getCurrentVersion(this);
let $buttonRef = null;

//https://youtu.be/pT2bSZlfQq0?si=VMhewAPAMuTK5TFy
const prefixes = ['https://www.youtube.com', 'https://youtu.be'];

const {plugins} = this.app.plugins;
const {createButton} = plugins["buttons"]
const yt = plugins['ytranscript'];

const makeOpenBtn = (container, url, name) => {
  return createButton({
    app,
    el: container,
    args: {
      name,
    },
    clickOverride: {
      click: openView.bind(this),
      params: [{
        url,
        getYtTabEl: getYtTabEl.bind(this),
        yt
      }],
    },
  })
}

//bootstrap
workspace.onLayoutReady(bootstrap.bind(this));

/**
 * Represents a URL context.
 * @typedef {Object} Link
 * @property {string} text
 */
/**
 * Represents a URL context.
 * @typedef {Object} UrlContext
 * @property {string} domain - The domain of the URL.
 * @property {Link} link - The domain of the URL.
 * @property {string} domain - The domain of the URL.
 */
function bootstrap() {
  makeOpenBtn(container, "", "Refresh " + VERSION);
  (async function(ctx) {
    const abstractFile = workspace.getActiveFile();
    const {listItems} = metadataCache
      .getFileCache(abstractFile);

    const cr = await vault.cachedRead(abstractFile)
    if (!listItems) return;

    const texts = getAllTextsFromListItems(
      listItems,
      cr
    );

    /**
    * @type {number}
    */
    const urlContext = findUrl(texts, prefixes);
    if (urlContext !== null) {
      return main.call(ctx, urlContext);
    }
  })(this)
}



function main(urlContext) {
  container.style = 'border: 3px solid lightblue;margin: .5em 0;'
  const row1 = [
    'YTranscript',
    '。。。。',
    makeOpenBtn.call(this, container,urlContext, 'Open')
  ];
  $buttonRef = row1[2];

  const md = dv.markdownTable('*,*,*'.split(","),[row1])
  const {link, domain, urlPath} = urlContext
  const _url = (domain + urlPath).trim()
  //getMarkdownALinkByUrl(url.trim())
  workspace.onLayoutReady(() => {
    dv.paragraph(`\`\`\`timestamp-url\n${_url}\n\`\`\``)
  })
}

function getAllTextsFromListItems(listItems,cr) {
  const crlines = cr.split('\n');
  const listItemTextsMatrix = [];
  for (const listItem of listItems) {
    const startLineIdx = listItem?.position?.start?.line
    const endLineIdx = listItem?.position?.end?.line
    const listItemTexts = crlines
      .slice(startLineIdx, endLineIdx + 1);
    listItemTextsMatrix.push(
      {text: listItemTexts.join("")}
    );
  }
  return listItemTextsMatrix;
}
function findUrl(links, domains) {
  const tuples = [];
  for (let link of links) {
    for (const domain of domains) {
      if (link?.text?.contains(domain)) {
        tuples.push({link,domain})
      }
    }
  }
  const tuple = tuples.findLast(
    ({link,domain}) => {
      // return link?.text.match(new RegExp("\\b" "s*\\*\\s*" + "\\b" + priority_prefix,"g"));
      // #_todo/to_document/on-coding/regarding-dynamic-regex
      const dynamicRegex = new RegExp(`\\s*\\*\\s*${priority_prefix}`, "g");
      const result = link?.text?.match(dynamicRegex);
      return result;
      //return link?.text.match(new RegExp(`\s*\*\s*${priority_prefix}`, "g"));
    }
  );
  if (!tuple) {
    return null
  }
  const {domain, link} = tuple;
  const urlPath =  link?.text?.split(domain)[1];
  const parsed_infos = [link, urlPath, domain]
  console.log({parsed_infos})
  if (!parsed_infos.every(Boolean)) {
    return null;
  }
  return {link, urlPath, domain};
}


function openView({url, yt, getYtTabEl}) {
  new Notice( $buttonRef ? 'has' : 'nope')
  const ytTab = getYtTabEl()
  if (!$buttonRef) {
    return;
  }
  if (ytTab?.tabHeaderCloseEl) {
    ytTab.tabHeaderCloseEl.click()
    $buttonRef.innerText = 'Open';
    return;
  }

  $buttonRef.innerText = 'Close';
  yt.openView(url)

}

function getYtTabEl() {
  return workspace.rightSplit.children[0]
    ?.children.find(findViewPredicate)
}

function findViewPredicate({tabHeaderEl}) {
  return tabHeaderEl?.dataset?.type === 'transcript-view'
}

function parseFrontmatter(frontmatter, key) {
  if (!Object.keys(frontmatter)?.length) {
    return;
  }
  return frontmatter[key] ?? "";
}

function getMarkdownALinkByUrl(url) {
  if (!url) return "";
  return `[](${url})`
}
```

# ---Transient

# ---Transient Doc Log

- v0.0.2
  - Archive prototype list
- ## Versioned Prototypes
  - [[list-of-prototypes,ad-finem-Video-notetaking,vis-Noteshippo]]
