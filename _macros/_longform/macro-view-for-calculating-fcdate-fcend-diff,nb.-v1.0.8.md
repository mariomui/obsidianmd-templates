
- 💁 See [[macro-view-for-calculating-fcdate-fcend-diff,nb.-v1.0.8]] for details

```dataviewjs
const MACRO_VERSION = italicize("v1.0.8")

const {default: obs} = this.app.plugins.plugins['templater-obsidian'].templater.current_functions_object.obsidian;

const {workspace, vault, metadataCache, fileManager} = this.app;

const vf = this.app.vault.getAbstractFileByPath(dv.currentFilePath)
const mdc = metadataCache.getFileCache(vf)

const MF = "YYYY/MM/DD"
const mfcstart = moment(mdc?.frontmatter?.['fc-date'], MF)
const mfcend = moment(mdc?.frontmatter?.['fc-end'],MF)
// const d = mfcDiff(mfcstart, mfcend, "days")
const y = mfcDiff(mfcstart, mfcend, "years")
// const m = mfcDiff(mfcstart, mfcend, "months")

const MDY = "**YYYY**/MM";
const isEvent = (mfcend.years() - mfcstart.years()) === 0;
const circa = `*from* ${mfcstart.format(MDY)} *to* ${mfcend.format(MDY)}`;

// I

const style = cls({ 
  "padding": "1em 1.2em",
  ["font-size"]: "1.2em"
});

// # BOOTSTRAP
workspace.onLayoutReady(main.bind(this));

// # MAIN LAYER 
function main() {

  // ## LOGIC LAYER

  // ## UI LAYER
  if (isEvent) {
    dv.el.call(
      this,
      "div",
      `POINT EVENT: ` + mfcstart.format(MDY) + ` ${MACRO_VERSION}`,
      style
    )
  } else {
    dv.el.call(
      this,
      "div",
      `... **spans** ${y}**yrs** ` + circa + ` ${MACRO_VERSION}`,
      style
    )
  }
  
  // ## CONCRETE RENDER UNIT TO SHOW SELECTED FRONTMATTER
  // ### DATA
  const _UNWANTEDS = [
    "fc-", "aat-", "MACRO_", 
    "_VERSION", "cssclasses", "timelines"
  ];

  // ### LOGIC
  const mapValueToField = (tuple) => {
      const [a,b] = tuple;
      return `* ${a}: ${Array.isArray(b) ? b.join(", ") : b}`;
  };
  const createFilterWithUnwantedsAccess = ( UNWANTEDS , cb) => {
    return function filterBy(element) {
      return cb(UNWANTEDS, element);
    }
  };
  const filterByUnwantedKeyField = createFilterWithUnwantedsAccess(
    _UNWANTEDS, 
    (_UNWANTEDS, tuple) => {
    
      const [k,v] = tuple;
      if (typeof v === "boolean") return false;
      if (v === null) return false;
      // if key includes anything in unwanted do not render
      return _UNWANTEDS.every(
        (unwanted) => (
          k.toLowerCase().indexOf(
            unwanted.toLowerCase()
          ) === -1
        )
      )
    }
  );
  // ### UI
  dv.list.call(
    this,
    Object.entries(mdc.frontmatter ||{})
      .filter(filterByUnwantedKeyField)
      .map(mapValueToField)
  );
}




// # UTIL

function italicize(target) {
  return `*${target}*`
}
function filterByB([a,b]) {
  return !!b;
}
function mfcDiff(mfcstart, mfcend, strat) {
  const res = mfcend.diff(mfcstart,strat)
  return res;
}

function cls(style = {}) {
  const _style = Object.entries(style).reduce(
    (chain, [a,b]) => {
      return chain += `${a}:${b};`
    },
    ""
  )
  return { 
    attr: {
      style: _style
    }
  }
}
```


<%* /** 
- v1.0.8 *2024-07-31*
  - onlayout to help queue with refreshing
  - 
- v1.0.7 *2024-07-30*
  - add the linkback to the original code for macro details.
  - seperate title level versioniong info to nb 
**/ -%>