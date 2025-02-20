---
aliases:
  - macro-for-inserting-file-basename-into-litnote
  - ø-macro-for-inserting-file-basename-into-litnote
---
**file_basename**: *`= this.file.name`* doc-`=this.DOC_VERSION` `= this.MUID`/`=this.heading`/`=this.UMID`/
**is-using-latest-template**: `= (([[litnote-template]].TEMPLATE_VERSION)=(this.file.frontmatter.TEMPLATE_VERSION)) `
