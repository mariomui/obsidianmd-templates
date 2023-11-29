---
---

# Bootup

```dataviewjs
this.app.workspace.onLayoutReady(
  main.bind(this)
);

function main() {
  if (!this.app?.mrender?.renderEl) {
    this.app.mrender = {}
  
    this.app.mrender.renderEl = renderEl
    function renderEl(_value = 0, max = 100) {
        const space = "&nbsp;"
        const progress_html = `<progress value="${_value}" max="${max}"></progress>${space.repeat(10)}<span>${((_value/max)*100).toFixed(2)}%</span>`
        const $p = this.container.createEl("p", {attr: {style: `margin: 0.2em 1em .2em 1em`}})
        $p.innerHTML = progress_html;
    }
  }
}

```
