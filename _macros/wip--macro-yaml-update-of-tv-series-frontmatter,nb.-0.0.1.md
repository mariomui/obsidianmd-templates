
<%*



tp.hooks.on_all_templates_executed(async () => {
    const fileView = tp.app.workspace.getActiveFileView()
    
    const metadataEditor = fileView.metadataEditor
    const serializeYaml = metadataEditor.serialize.bind(metadataEditor);
    const synchronizeYaml = metadataEditor.synchronize.bind(metadataEditor);
    
    const MEDIA_DB = tp.app.plugins.plugins["obsidian-media-db-plugin"]
    const SERIES_API = MEDIA_DB.apiManager.apis.first();
    const MODEL_MANAGER = MEDIA_DB.modelPropertyMapper;
    const MODAL_HELPER = MEDIA_DB.modalHelper;
    const API_MANAGER = MEDIA_DB.apiManager


    await genMain({
      fileView, serializeYaml, metadataEditor, synchronizeYaml, SERIES_API, MODEL_MANAGER, MODAL_HELPER, API_MANAGER, MEDIA_DB
    })
    .catch(console.log)
})

async function genMain(pkg) {
  const {
      fileView, serializeYaml, metadataEditor, synchronizeYaml, SERIES_API, MODEL_MANAGER, MODAL_HELPER, API_MANAGER, MEDIA_DB
  } = pkg;

  
  const fm = serializeYaml();
  

  const apiSearchResults = await createEntryWithAdvancedSearchModal
    .call(
      MODAL_HELPER,
      API_MANAGER, 
      MEDIA_DB
    );



  /**
  const prompt = await genPrompt()
  const isId = prompt.payload.startsWith("idx")

  const data = !isId ? await genDataByTitle(prompt.payload) :  await genDataById(prompt.payload)
  
  async function genDataByTitle(title) {
    const resp = await SERIES_API.searchByTitle(title.slice(3))
  
    const titles = resp.map((r) => `${r.englishTitle} ${r.type} ${r.year}`)
    
    const choice = await tp.system.suggester(titles, resp)
    const data = await SERIES_API.getById(choice.id)
    return data
  }
  async function genDataById(id) {
    const data = await SERIES_API.getById(id)
    return data
  }
  **/
  
  // has userData in a {}
  if (!apiSearchResults.length) return;
  const apiSearchResult = apiSearchResults.first()
  const { userData } = apiSearchResult;

  const updatedFm = syncFmWithUserData(
    fm,
    {...userData, "BANNER_y": 50 } // custom user data
  );
  
  const update = apiSearchResult.getWithOutUserData()
  //toMetaDataObject (eh)
  
  const mapped_update = MODEL_MANAGER.convertObject(update)
  const aboutToBeYaml = { ...updatedFm, ...mapped_update };

  const genSynchronizeYaml = createGenFrontmatterHelper(4000)
  const genSortYaml = createGenFrontmatterHelper(2000)


  await genSynchronizeYaml(
    aboutToBeYaml, 
    () => {
      synchronizeYaml(aboutToBeYaml)
    }
  ).catch((err) => {
    throw new Error(JSON.stringify({err, desc: "genSynchronizeYaml error"}))
  })
  metadataEditor.save()



  await genSortYaml( aboutToBeYaml, () => {
    tp.app.commands.executeCommandById(
      "obsidian-one-ring:sort frontmatter"
    )
  }).catch((err) => {
    throw new Error(JSON.stringify({err, desc: "gensortyaml error"}))
  })
  metadataEditor.save()

  fileView.editor.refresh()

  function createGenFrontmatterHelper(_timeout = 2000) {

    return function genHelper(inyaml, cb, timeout = _timeout) {
      return new Promise((resolve,reject) => {
      

        cb()
        setTimeout(() => {
          let ykeys = {}
          const currentYaml = serializeYaml()
          const inyamlLen = Object.keys(inyaml).length
          const currentYamlLen  = Object.keys(
            currentYaml
          ).length;
          // never fail
          resolve({isPass: true, pkg: null})
          /**
          if (currentYamlLen <= inyamlLen) {
            resolve({isPass: true, pkg: null})
          } else {
            for ( let k in inyaml) {
              if (!currentYamlLen.hasOwnPropery(k)) {
                ykeys[k] = inyaml[k]
              }
            }
            reject({
              isPass: false,
              pkg: Object.keys(inyaml)
             })
          }
          **/
        }, timeout)
  
      })
    }
  }

  // without the view refreshing, the frontmatter doesn't display.
  // in here, i refresh using a save 


  function syncFmWithUserData(fm, userData) {
    // if current fm has userData leave alone, if not add to thingie.
    const pkg = { ...fm }
    const insert = {}
    for (let key in userData) {
      const isEmpty = [null,undefined].includes(pkg[key]) || !pkg.hasOwnProperty(key);
      console.log({isEmpty, key})
      if (isEmpty) {
      // in order to sync, the frontmatter must be pre-told of the change. 
        insert[key] = userData[key]
      }
    }
    metadataEditor.insertProperties(insert)
    metadataEditor.save()
    return { ...pkg, ...insert };
  }
}

async function createEntryWithAdvancedSearchModal(
  API_MANAGER, MEDIA_DB
) {
  const apiSearchResults = await this
  .openAdvancedSearchModal({}, async advancedSearchModalData => {
    return await API_MANAGER.query(
      advancedSearchModalData.query, 
      advancedSearchModalData.apis
    );
  });

  if (!apiSearchResults) {
    // TODO: add new notice saying no results found?
    return;
  }

  let selectResults;
  let proceed = false;

  while (!proceed) {
    selectResults =
      (await this.openSelectModal(
        { elements: apiSearchResults }, 
        async selectModalData => {
          return await MEDIA_DB
            .queryDetails
            .call(MEDIA_DB, selectModalData.selected);
        }
      )
    ) ?? [];
    if (!selectResults) {
      return;
    }

    proceed = await this.openPreviewModal(
      { elements: selectResults }, 
      async previewModalData => {
        return previewModalData.confirmed;
      }
    );
  }

  return selectResults
}

async function genPrompt() {
  const pkg = {
    processing: true,
    payload: null,
  }
  const request_string = await tp.system.prompt("What's the tv series called", null, true)
  pkg.payload = request_string;
  pkg.processing = false;
  return pkg;
}

/** Commit Log
* v0.0.2 *2025-01-25*
  * Replace my own modals with mediadb modals and expanding it to all mediums not just series.
* v0.0.1 *2025-01-24*
  * Some idiosyncracies with metadataEditor synchronize. Synchronize by itself does not update the original yaml manifest. The setter functions call save into state. And only then does it set the properties. Infact. It makes no sense to use synchronize but use insertProperties for new items. Synchronize is for two exact copies to sync the old template with new template data. It's not a true sync. More like a structured overwrite with schema enforcement.
  * save is important to save to the obsidian internal model.
  * I thought that modifying the text would trigger Note refresh but no. Codemirror requires programmatic refresh.
    * tp.workspace.getActiveFileView().editor.refresh() triggers Codemirror to update
**/
_%>
