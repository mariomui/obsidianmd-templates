<%*
// MUID-3117
tp.hooks.on_all_templates_executed(() => {
  const CSS_FIELD = "cssclasses";
  const CSS_VALUE = "colorGrammar";
  const tfile = tp.file.find_tfile(
    tp.file.path(true)
  );
  // const cache = tp.app.metadataCache.getFileCache(tfile);  

  tp.app.fileManager.processFrontMatter(tfile, (fm) => {
    console.log({fm})
    const cssVal = fm?.[CSS_FIELD];
    <!-- fm[CSS_FIELD] = 2; -->
    if (cssVal === undefined) {
      fm[CSS_FIELD] = [CSS_VALUE]
      return;
    }
    if (cssVal?.length === 0) {
      fm[CSS_FIELD].push(CSS_VALUE)
      return
    }
    if (cssVal === null) {
      fm[CSS_FIELD] = [CSS_VALUE]
      return
    }
    if (cssVal) {
      delete fm[CSS_FIELD]
      return
    }
  })
})
-%>
