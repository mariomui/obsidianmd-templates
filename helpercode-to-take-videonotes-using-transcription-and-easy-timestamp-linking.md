---
alias:
TEMPLATE_VERSION: v1.0.4_video-note-taking
DOC_VERSION: v0.0.1
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
### References
* https://www.youtube.com/example
* [[√-LEADERSHIP-LAB-Writing-Beyond-the-Academy-1-23-15-YouTube-https-www-youtube-com-watch-v=aFwVf5a3pZM]] has some code to properly include the Youtube Transcripting Code without running into dataview issues.   

# =
## Transcript Control

```dataviewjs
// v1.0.4
const {default: obs} = this.app.plugins.plugins['templater-obsidian'].templater.current_functions_object.obsidian

const {workspace,metadataCache, vault} = this.app;
const {container} = this;


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

const prefix = 'https://www.youtube.com';

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

workspace.onLayoutReady(bootstrap.bind(this));

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
    const url = findUrl(texts, prefix);

    // dv.paragraph(prefix + url)

    if (url?.length) {
      return main.call(ctx, prefix + url);
    }
  })(this)
}



function main(url) {
  container.style = 'border: 3px solid lightblue;margin: .5em 0;'
  const row1 = [
    'YTranscript',
    '。。。。',
    makeOpenBtn.call(this, container,url, 'Open')
  ];
  $buttonRef = row1[2];

  const md = dv.markdownTable('*,*,*'.split(","),[row1])
  //dv.paragraph(md);
  dv.paragraph(`\`\`\`timestamp-url\n${url}\n\`\`\``)
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
function findUrl(links, sep) {

  const found = links?.findLast(
    (link) => {
      return link?.text?.contains(sep)
    }
  );
  return found?.text?.split(sep)[1];
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
```

# ---Transient

## v1
```js
~~~dataviewjs
const {vault, metadataCache} = this.app;
let $buttonRef = null;
const {file: {lists} }= dv.current();
const links = lists.values;
const source_path = this.currentFilePath
const sourcedAbstractFile = vault
  .getAbstractFileByPath(source_path);
const {frontmatter} = metadataCache.getFileCache(sourcedAbstractFile);

function parseFrontmatter(frontmatter, key) {
  if (!Object.keys(frontmatter)?.length) {
    return;
  }
  return frontmatter[key] ?? "";
}
const VERSION = parseFrontmatter(frontmatter, "VERSION");
const prefix = 'https://www.youtube.com';
const url = findUrl(links, prefix)
console.log({url})
function findUrl(links, sep) {
    const found = links?.findLast((link) => {
        return link?.text?.contains(sep)
    })
    return found?.text?.split(sep)[1];
}


const {plugins} = this.app.plugins
const {createButton} = plugins["buttons"]
const yt = plugins['ytranscript'];

const makeOpenBtn = (container, url, name) => createButton({ 
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

makeOpenBtn(
  this.container,
  "", 
  `Refresh ${VERSION}`
);

if (url?.length) {
    console.log({url})
    ubermain(
        main.bind(this), prefix + url)
}



function ubermain(main, url) {
    console.log({url})
    main(url);
}

function main(url) {
    this.container.style = 'border: 3px solid lightblue;margin: .5em 0;'
    const row1 = [
        'YTranscript',
        '。。。。',
        makeOpenBtn(this.container,url, 'Open')
    ];
    $buttonRef = row1[2]
    dv.table(
        '',
        [
            row1,
        ],
    )

    

}
function openView({url, yt, getYtTabEl}) {

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
    return this.app.workspace.rightSplit
        .children[0]
        ?.children
        .find(findViewPredicate)   
}
function findViewPredicate({tabHeaderEl}) {
    return tabHeaderEl
            ?.dataset?.type 
                === 'transcript-view'
}
~~~
```

---
## v2

- [ ] Do a diff betweeen v1 and v2 and see if they are the same.
```js

~~~
dataviewjs
let $buttonRef = null;
const links = dv.current().file.lists.values;
console.log({links})

const prefix = 'https://www.youtube.com';
const url = findUrl(links, prefix)
function findUrl(links, sep) {
    const found = links?.findLast((link) => {
        return link?.text?.contains(sep)
    })
    return found?.text?.split(sep)[1];
}


const {plugins} = this.app.plugins
const {createButton} = plugins["buttons"]
const yt = plugins['ytranscript'];

const makeOpenBtn = (container, url, name) => createButton({ 
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

makeOpenBtn.call(this,this.container, "", "Refresh");
if (url?.length) {
    console.log({url})
    ubermain(
        main.bind(this), prefix + url)
}



function ubermain(main, url) {
    console.log({url})
    main(url);
}

function main(url) {
    this.container.style = 'border: 3px solid lightblue;margin: .5em 0;'
    const row1 = [
        'YTranscript',
        '。。。。',
        makeOpenBtn(this.container,url, 'Open')
    ];
    $buttonRef = row1[2]
    dv.table(
        '',
        [
            row1,
        ],
    )

    

}
function openView({url, yt, getYtTabEl}) {

    const ytTab = getYtTabEl()
    console.log(this.container, 'button')
    if (ytTab?.tabHeaderCloseEl) {
        ytTab.tabHeaderCloseEl.click()
        $buttonRef.innerText = 'Open';
console.log($buttonRef.previousSibling);
    } else {
        $buttonRef.innerText = 'Close';
        yt.openView(url)
    }
}  
function getYtTabEl() {
    return this.app.workspace.rightSplit
        .children[0]
        ?.children
        .find(findViewPredicate)   
}
function findViewPredicate({tabHeaderEl}) {
    return tabHeaderEl
            ?.dataset?.type 
                === 'transcript-view'
}

~~~
```

## v3

```js
~~~dataviewjs

let $buttonRef = null;
const links = dv.current().file.lists.values;
console.log({links})

const prefix = 'https://www.youtube.com';
const url = findUrl(links, prefix)
function findUrl(links, sep) {
    const found = links?.findLast((link) => {
        return link?.text?.contains(sep)
    })
    return found?.text?.split(sep)[1];
}


const {plugins} = this.app.plugins
const {createButton} = plugins["buttons"]
const yt = plugins['ytranscript'];

const makeOpenBtn = (container, url, name) => createButton({ 
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

makeOpenBtn(this.container, "", "Refresh");
if (url?.length) {
    console.log({url})
    ubermain(
        main.bind(this), prefix + url)
}



function ubermain(main, url) {
    console.log({url})
    main(url);
}

function main(url) {
    this.container.style = 'border: 3px solid lightblue;margin: .5em 0;'
    const row1 = [
        'YTranscript',
        '。。。。',
        makeOpenBtn(this.container,url, 'Open')
    ];
    $buttonRef = row1[2]
    dv.table(
        '',
        [
            row1,
        ],
    )

    

}
function openView({url, yt, getYtTabEl}) {

    const ytTab = getYtTabEl()
    console.log(this.container, 'button')
    if (ytTab?.tabHeaderCloseEl) {
        ytTab.tabHeaderCloseEl.click()
        $buttonRef.innerText = 'Open';
console.log($buttonRef.previousSibling);
    } else {
        $buttonRef.innerText = 'Close';
        yt.openView(url)
    }
}  
function getYtTabEl() {
    return this.app.workspace.rightSplit
        .children[0]
        ?.children
        .find(findViewPredicate)   
}
function findViewPredicate({tabHeaderEl}) {
    return tabHeaderEl
            ?.dataset?.type 
                === 'transcript-view'
}
~~~
```

## v4 (i know this one works)

I took an old back up just to make sure i didn't eff up.
```js
~~~dataviewjs
let $buttonRef = null;
const links = dv.current().file.lists.values;

const prefix = "https://www.youtube.com";

const url = findUrl(links, prefix);
function findUrl(links, sep) {
  const found = links?.findLast((link) => {
    return link?.text?.contains(sep);
  });
  return found?.text?.split(sep)[1];
}

const { plugins } = this.app.plugins;
const { createButton } = plugins["buttons"];
const yt = plugins["ytranscript"];

const makeOpenBtn = (container, url, name) =>
  createButton({
    app,
    el: container,
    args: {
      name,
    },
    clickOverride: {
      click: openView.bind(this),
      params: [
        {
          url,
          getYtTabEl: getYtTabEl.bind(this),
          yt,
        },
      ],
    },
  });
makeOpenBtn(this.container, "", "♻");
if (url?.length) {
  console.log({ url });
  ubermain(main.bind(this), prefix + url);
}

function ubermain(main, url) {
  console.log({ url });
  main(url);
}

function main(url) {
  this.container.style = "border: 3px solid lightblue;margin: .5em 0;";
  const row1 = [
    "YTranscript",
    "。。。。",
    makeOpenBtn(this.container, url, "Open"),
  ];
  $buttonRef = row1[2];
  dv.table("", [row1]);
}
function openView({ url, yt, getYtTabEl }) {
  const ytTab = getYtTabEl();
  console.log(this.container, "button");
  if (ytTab?.tabHeaderCloseEl) {
    ytTab.tabHeaderCloseEl.click();
    $buttonRef.innerText = "Open";
    console.log($buttonRef.previousSibling);
  } else {
    $buttonRef.innerText = "Close";
    yt.openView(url);
  }
}
function getYtTabEl() {
  return this.app.workspace.rightSplit.children[0]?.children.find(
    findViewPredicate,
  );
}
function findViewPredicate({ tabHeaderEl }) {
  return tabHeaderEl?.dataset?.type === "transcript-view";
}
~~~
```


# ---Transient v2023-06-08


```js
~~~dataviewjs
let $buttonRef = null;
const links = dv.current().file.lists.values;


const prefix = 'https://www.youtube.com';
const url = findUrl(links, prefix)
function findUrl(links, sep) {
    const found = links?.findLast((link) => {
        return link?.text?.contains(sep)
    })
    return found?.text?.split(sep)[1];
}


const {plugins} = this.app.plugins
const {createButton} = plugins["buttons"]
const yt = plugins['ytranscript'];

const makeOpenBtn = (container, url, name) => createButton({ 
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

if (url?.length) {
    console.log({url})
    ubermain(
        main.bind(this), prefix + url)
}



function ubermain(main, url) {
    main(url);
}

function main(url) {
    this.container.style = 'border: 3px solid lightblue;margin: .5em 0;'
    const row1 = [
        'YTranscript',
        '。。。。',
        makeOpenBtn(this.container,url, 'Open')
    ];
    $buttonRef = row1[2]
    dv.table(
        '',
        [
            row1,
        ],
    )

    

}
function openView({url, yt, getYtTabEl}) {

    const ytTab = getYtTabEl()
    console.log(this.container, 'button')
    if (ytTab?.tabHeaderCloseEl) {
        ytTab.tabHeaderCloseEl.click()
        $buttonRef.innerText = 'Open';
console.log($buttonRef.previousSibling);
    } else {
        $buttonRef.innerText = 'Close';
        yt.openView(url)
    }
}  
function getYtTabEl() {
    return this.app.workspace.rightSplit
        .children[0]
        ?.children
        .find(findViewPredicate)   
}
function findViewPredicate({tabHeaderEl}) {
    return tabHeaderEl
            ?.dataset?.type 
                === 'transcript-view'
}
~~~
```

# ---Transient Commitlog