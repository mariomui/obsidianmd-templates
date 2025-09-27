
<%*
// MUID-3136
// do not bump version.

const ɵomdbApiType = {
	SERIES: "series"
}
tp.hooks.on_all_templates_executed(
	async () => {
		const fileView = tp.app.workspace.getActiveFileView()

		const metadataEditor = fileView.metadataEditor
		const serializeYaml = metadataEditor.serialize.bind(metadataEditor);
		const synchronizeYaml = metadataEditor.synchronize.bind(metadataEditor);
		
		const MEDIA_DB = tp.app.plugins.plugins["obsidian-media-db-plugin"]
		
		const SERIES_API = MEDIA_DB.apiManager.apis.first();
		// 🔗 https://github.com/mProjectsCode/obsidian-media-db-plugin/blob/73c9391416566242d5de61667a21244136233bd5/src/main.ts#L53 
		/** 🆙
		Series api manager implementation is 🐛prone because it depends on knowing that the first api registered is OMDBApi
		Consider MEDIADB.apiManager.apis.find((api) => api.apiName === "OMDBApi"))
		**/		
		const MODEL_MANAGER = MEDIA_DB.modelPropertyMapper;
		const MODAL_HELPER = MEDIA_DB.modalHelper;
		const API_MANAGER = MEDIA_DB.apiManager

		await genMain({
			fileView, serializeYaml, metadataEditor, synchronizeYaml, SERIES_API, MODEL_MANAGER, MODAL_HELPER, API_MANAGER, MEDIA_DB
		})
		.catch(console.log)
	}
);

async function genMain(pkg) {
	const {
		fileView, serializeYaml, metadataEditor, synchronizeYaml, SERIES_API, MODEL_MANAGER, MODAL_HELPER, API_MANAGER, MEDIA_DB
	} = pkg;

	const fm = serializeYaml();

	// call createEntry with context to modal_helper so that i can use its context.
	const apiSearchResults = await createEntryWithAdvancedSearchModal
		.call(
			MODAL_HELPER,
			API_MANAGER,
			MEDIA_DB
		);

	// ! DO NOT USE the getById stuff from their mediaDB, mofo only supports a sliver of available api. Wait till someone updates it.
	
	// has userData in a {}
	if (!apiSearchResults.length) return;
	
	const apiSearchResult = apiSearchResults.first()
	
	const isTelevisionSeries = apiSearchResult && apiSearchResult.type === ɵomdbApiType.SERIES;
	// if it's a series, make sure that we populate the user Data with episode specific data.

	const { userData } = apiSearchResult;
	const seriesMapping = new Map();
	
	const yesNoFig = {
		Yes: true, No: false
	}
	const wantMoreEpisodeDateChoice = isTelevisionSeries && await tp.system.suggester(
		(choice) => choice, ["Yes", "No"], false, "Want episode data?"
	);
	
	const isAllowedToGrabMoreTVInfo = yesNoFig[wantMoreEpisodeDateChoice];

	if (isAllowedToGrabMoreTVInfo) {
		// https://www.omdbapi.com/?apikey=[YOURKEY]&season=1&episode=4&i=tt16027014
		
		const omdb_series_id = apiSearchResult.id;
		
		// create modal for using the seasons then ask for episode count.
		const season_label_choice = await tp.system.prompt("What season?");
		const episode_label_choice = await tp.system.prompt("What episode do you want?")

		const omdbApiFig = {
			api_key : MEDIA_DB.settings.OMDbKey,
			api_url :	"https://www.omdbapi.com"
		}
		const tvEpisodeQueryFig = {
			episode: episode_label_choice || "",
			season: season_label_choice || "",
			i: omdb_series_id
		}
		const tvSeasonQueryFig = {
			season: season_label_choice || "",
			i: omdb_series_id
		}

		const episodeResp = await genFetchMediaInfoBy( omdbApiFig, tvEpisodeQueryFig);

		const seasonResp = await genFetchMediaInfoBy( omdbApiFig, tvSeasonQueryFig).catch(console.log)
		const episode_cnt = seasonResp?.json?.["Episodes"]?.length || 0

		const api_date_format = 'DD MMM YYYY';

		const fieldnameFig = {
	      "Title" : {
					label: "episodeTitle",
					type: "label"
				},
	      "Rated" : {
					label: "contentAdvisory",
					type: "label"
				},
	      "Released": {
					label: "airedFrom",
					type: "date"
				},
	      "Season": {
					label: "season_no",
					type: "number"
				},
	      "Episode": {
					label: "episode_no", 
					type: "number"
				},
	      "Runtime": {
					label: "duration",
					type: "label"
				},
	      "Genre": {
					label: "genres",
					type: "array"
				},
	      "Director": {
					label: "director",
				},
	      "Writer": {
					label: "writer",
					type: "array"
				},
	      "Actors": {
					label: "actors",
					type: "array"
				},
	      "Plot": {
					label: "plot",
				},
	      "Language": {
					label: "language",
				},
	      "Country": {
					label: "country",
				},
	      "Poster": {
					label: "BANNER",
					type: "image"
					//image: result.Poster.replace('_SX300', '_SX600'),
				},
	      "imdbID": {
					label: "id",
				},
	      "seriesID": {
					label: "seriesId",
				},
	      "Type": {
					label: "type"
				}
		}

		const asis = (text) => text;
		const formatterByTypeFig = {		
			array: (x) => x.split(","),
			image: (x) => x.replace("_SX300", "_SX600"),
			number: (x) => Number(x) || 0,
			label: asis,
			date: (x) => MEDIA_DB.dateFormatter.format(x, api_date_format)
		}
		for (let resp_key in fieldnameFig) {
			const resp_data = episodeResp.json[resp_key] || "";
			
			const fig = fieldnameFig[resp_key];
			const { label, type } = fig;
			
			const formatter = formatterByTypeFig[type] || asis;
			const formatted_data = formatter(resp_data);
			seriesMapping.set(label, formatted_data)
		}
		seriesMapping.set("episodes", episode_cnt);
	}
	
	const updatedFm = syncFmWithUserData(
		fm,
		{...userData, "BANNER_y": 50 } // custom user data
	);

	const update = apiSearchResult.getWithOutUserData()
	const tvseriesUpdate = Object.fromEntries(seriesMapping);
	
	const mapped_update = MODEL_MANAGER.convertObject(
		{ 
			...update, 
			...tvseriesUpdate, // override apiSearchResult entry
		}
	);
	console.log({mapped_update, seriesMapping})
	const aboutToBeYaml = { 
		...updatedFm, // this one has my custom private settings
		...mapped_update,  // this one has no userData so no conflict with above
	};
	//console.log({aboutToBeYaml})
	
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
		setTimeout(() => {
			tp.app.commands.executeCommandById(
				"obsidian-one-ring:sort frontmatter"
			);
		fileView.editor.refresh();
		},1000)
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
			// console.log({isEmpty, key})
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

/**
	@return selectResults : Array<mediaInfo>
**/
async function createEntryWithAdvancedSearchModal(
	API_MANAGER, MEDIA_DB
) {
	const apiSearchResults = await this
	.openAdvancedSearchModal({}, async advancedSearchModalData => {
		const selected_searchby_title = advancedSearchModalData.query;

		return await API_MANAGER.query(
			selected_searchby_title,
			advancedSearchModalData.apis // This is usually OMDBApi as determined by the API names
		);
	});

	if (!apiSearchResults) {
		// TODO: add new notice saying no results found?
		return;
	}
	
	// console.log({apiSearchResults}) Lists the results for secondary modal selection process
	// If it is type series, produce a tertiary modal.
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

		// console.log({selectResults}) 
		// selectResults: Array<mediaInfo>
		
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

async function genFetchMediaInfoBy(apiFig, queryFig) {
	const { api_key, api_url } = apiFig
  
	const theUrl = new URL(api_url);
	
	const query_string = new URLSearchParams({
		apikey: api_key,
	...queryFig,
	}).toString();

	theUrl.search = query_string
	const resp = await tp.obsidian.requestUrl(theUrl.toString());
	if (resp.status !== 200) {
		throw new Error(JSON.stringify({resp}) + "requestURL not working")
	}
	return resp;
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
