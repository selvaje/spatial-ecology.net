---
layout: page-fullwidth
classes: wide
title: "Environment90m layers"
meta_title: "Env90m"
permalink: "/environment90m/environment90m_layers"
header:
   image_fullwidth: "yusdiel_streifen5.jpg"
---

We recently prepared a new dataset called Environment90m!

For each of the roughly <b>726 million sub-catchments</b> present in Hydrography90m, it provides <b>detailed data on soil condition, bioclimatic variables, land cover, and many more.</b> Just like the Hydrography90m layers, it is openly available for download, and easy to download using the dedicated functions in the <b>R package</b> <a href="https://glowabio.github.io/hydrographr/" target="_blank">hydrographr</a>.

Here is an overview of all tables in the dataset. It consists of the summary statistics of <b>112 environmental layers in 7 categories</b> which we calculated for each single sub-catchment of the <a href="../hydrography90m/hydrography90m_layers">Hydrography90m dataset</a> (<em>Amatulli et al. (2022)</em>, see <a href="#references">references</a> below).


Please see the paper by <em>Garcia Marquez et al. (2026)</em> for further details (see <a href="#references">references</a> below).


* <a href="/environment90m/environment90m_layers#esa">Land Cover</a>
* <a href="/environment90m/environment90m_layers#chelsa">Bioclimatic variables</a>
* <a href="/environment90m/environment90m_layers#soil">Soil</a>
* <a href="/environment90m/environment90m_layers#flo1k">Stream Flow</a>
* <a href="/environment90m/environment90m_layers#meritdem">Elevation</a>
* <a href="/environment90m/environment90m_layers#cgiar">Aridity and Evapotranspiration</a>
* <a href="/environment90m/environment90m_layers#hy90m">Hydrography90m variables</a>

For downloading and working with the data, we recommend using the <b>R package</b> <a href="https://glowabio.github.io/hydrographr/" target="_blank">hydrographr</a>. Examples of how to do this are included below. A full <b>vignette</b> showing how to prepare and process the data needed to run a <b>species distribution model</b> to predict the habitat suitability of a fish species in a specific basin can be found at <a href="https://glowabio.github.io/hydrographr/articles/case_study_Danube.html" target="_blank">https://glowabio.github.io/hydrographr/articles/case_study_Danube.html</a>.

Please note that the dataset is protected by the Creative Commons Attribution-Non-Commercial 4.0 International License (<a href="http://creativecommons.org/licenses/by-nc/4.0">CC BY-NC 4.0</a>).

If you use our dataset in a publication, please also cite our work as:

* García Márquez, J. R., Grigoropoulou, A., Tomiczek, T., Schürz, M., Bremerich, V., Torres-Cambas, Y., Buurman, M., Amatulli, G., and Domisch, S. (2026): <b>Environment90m</b> - globally standardized environmental variables for freshwater science at high spatial resolution. Earth System Science Data, 18, 1541-1559, <a href="https://doi.org/10.5194/essd-18-1541-2026" target="_blank">doi:10.5194/essd-18-1541-2026</a>.


Citations of the work used to prepare this datasets can be found <a href="#references">at the bottom of this page</a>.

<!-- CSS styling -->
<style>
	table, th, td {border: 0px solid black; background-color: white;}

	.tileDownloadBoundsTitle {
		padding-bottom: 5px;
	}

	.mapTileDownloadContainer {
		width: 685px;
		height: 267px;
		display: block;
		position: relative;
	}

	.mapTileDownloadBaseLayer {
		position: absolute;
		left:0;
		right:0;
	}

	.tile {
		width:34px;
		height:34px;
		border:1px solid #606060;
		display:block;
		position:absolute;
		background-color: rgba(128,128,128,0.01);
	}

	.tile:hover {
		border:2px solid red;
		z-index:2;
		background-color: rgba(128,128,128,0.01);
	}

	.tile.selected {
		border:1px solid red;
		opacity: 0.6;
		z-index:2;
		background-color: red;
	}

	#tilepaths a {
		font-family: monospace;
		font-size: 10px;
	}

	#tilepaths a:link {
		text-decoration: none;
	}

	#tilepaths a:visited {
		text-decoration: none;
	}

	#tilepaths a:hover {
		text-decoration: underline;
	}

	#tilepaths a:active {
		text-decoration: underline;
	}

	div.anchorcontainer {
		position: relative;
		height:20px;
	}

	.th1 {
		font-size: 25px;
	}

	.th2 {
		font-size: 18px;
	}

	code {
		font-weight: bold;
	}

	/* Putting selection buttons on one line instead of newline: */
	.radio-buttons {
		display: flex;
		flex-wrap: wrap;   /* ← this allows line breaks */
		gap: 1em; /* adds spacing between buttons */
	}

	.radio-buttons input[type="radio"] {
		display: none; /* hide the actual radio input */
	}

	.radio-buttons label {
		padding: 0.2em 0.8em;
		border: 2px solid #ccc;
		border-radius: 4px;
		cursor: pointer;
		user-select: none;
		background-color: white;
		color: #333;
		transition: background-color 0.2s, border-color 0.2s;
	}

	/* Selected radio button: */
	.radio-buttons label.selected {
		color: #007bff;
		border-color: #007bff;
		font-weight: bold;
	}
	/* Greyed radio button: */
	.radio-buttons label.disabled {
		opacity: 0.5;           /* fade out the label */
		cursor: not-allowed;    /* show disabled cursor */
		pointer-events: none;   /* prevent clicks on the label itself */
	}

	.radio-buttons label:hover {
		background-color: #f0f0f0;
	}

	.code {
		background: #f4f4f4;
		border: 1px solid #ddd;
		color: #666;
		font-family: monospace;
		line-height: 1.6;
	}

	.cite {
		background: #fafafa;
		border: 1px solid #ddd;
		border-left: 3px solid #838383;
		page-break-inside: avoid;
		font-size: 15px;
		line-height: 1.6;
		margin-bottom: 1.6em;
		width: 935px;
		max-width: 100%;
		overflow: auto;
		#padding: 1em 1.5em;
		padding-left: 10px;
		padding-top: 10px;
		padding-right: 10px;
		display: block;
		word-wrap: break-word;
	}

	.codeblock {
		background: #f4f4f4;
		color: #666;
		border: 1px solid #ddd;
		border-left: 3px solid #70bfdb;
		page-break-inside: avoid;
		font-family: monospace;
		font-size: 15px;
		line-height: 1.6;
		margin-bottom: 1.6em;
		width: 935px;
		max-width: 100%;
		overflow: auto;
		#padding: 1em 1.5em;
		padding-left: 10px;
		padding-top: 10px;
		padding-right: 10px;
		display: block;
		word-wrap: break-word;
	}
</style>

<script src="../../pages/hydrography90m/jquery-3.6.0.js" type="text/javascript"></script>

<!-- Functions to update download paths upon clicking tile map or other buttons that modify what will be downloaded: -->
<script>
	try {
	console.log("Before defining set_path functions, jquery needs to be loaded!");
	if (typeof $ === 'undefined') {
		console.error('jQuery is not loaded!');
	} else {
		console.log('jQuery is loaded.');
	}

	console.log("DEBUG: Defining various functions to set paths...");

	try {
		console.log("DEBUG: Defining set_paths_bioclim...");
		function set_paths_bioclim(h, v, time_period, model, scenario) {
			h = String("00" + h).slice(-2);
			v = String("00" + v).slice(-2);
			let category = "chelsa_bioclim_v2_1";
			console.log(`DEBUG: Setting tile links for "${category}" (tile h${h}v${v}, period ${time_period}, model ${model}, scenario ${scenario})...`);
			let url_public = "https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ/download?path=%2F";
			var vars = ["bio01", "bio02", "bio03", "bio04", "bio05", "bio06", "bio07", "bio08", "bio09", "bio10",
					  "bio11", "bio12", "bio13", "bio14", "bio15", "bio16", "bio17", "bio18", "bio19"];

			/* Create download links, depending on whether it is observed or projected: */
			if (time_period === "1981-2010_observed") {
				/* Links like: "/1981-2010_observed/bio01/bio01_1981-2010_observed_h18v04.zip" */
				for (var i = 0; i < vars.length; i++) {
					let variable = vars[i];
					let time_period_only = time_period.replace('_observed','');
					let dyn_link =`<div>Download tile h${h}v${v} for time_period ${time_period} here: <br>
						<a href="${url_public}${category}/${time_period}/${variable}/${variable}_${time_period}_h${h}v${v}.zip" target="_blank">
						         ${url_public}${category}/${time_period}/${variable}/${variable}_${time_period}_h${h}v${v}.zip</a><br></div>`;
					$(`#dynamic_${variable}`).html(dyn_link);
				};
			} else {
				/* Links like: "/1981-2010_observed/bio01/bio01_1981-2010_ipsl-cm6a-lr_ssp126_v2_1_h18v04.zip" */
				for (var i = 0; i < vars.length; i++) {
					let variable = vars[i];
					let time_period_only = time_period.replace('_projected','').replace('_observed','');
					let dyn_link =`<div>Download tile h${h}v${v} for time_period ${time_period}, model ${model} and scenario ${scenario} here: <br>
						<a href="${url_public}${category}/${time_period}/${variable}/${variable}_${time_period_only}_${model}_${scenario}_v2_1_h${h}v${v}.zip" target="_blank">
						         ${url_public}${category}/${time_period}/${variable}/${variable}_${time_period_only}_${model}_${scenario}_v2_1_h${h}v${v}.zip</a><br></div>`;
					$(`#dynamic_${variable}`).html(dyn_link);
				};
			};
		};
		console.log("DEBUG: set_paths_bioclim defined");
	} catch (e) {
		console.error("Error defining set_paths_bioclim:", e);
	}

	try {
		console.log("DEBUG: Defining set_paths_landcover...");
		function set_paths_landcover(h, v, year) {
			h = String("00" + h).slice(-2);
			v = String("00" + v).slice(-2);
			let category = "esa_cci_landcover_v2_1_1";
			console.log(`DEBUG: Setting tile links for "${category}" (tile h${h}v${v}, year ${year})...`);
			let url_public = "https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ/download?path=%2F";
			var vars = [ "c10",  "c20",  "c30",  "c40",  "c50",  "c60",  "c70",  "c80",  "c90", "c100",
					  "c110", "c120", "c130", "c140", "c150", "c160", "c170", "c180", "c190", "c200",
					  "c210", "c220"];
			for (var i = 0; i < vars.length; i++) {
				var variable = vars[i];
				let dyn_link =`<div>Download tile h${h}v${v} for year ${year} here: <br>
					<a href="${url_public}${category}/${variable}/${variable}_${year}_h${h}v${v}.zip" target="_blank">
					${url_public}${category}/${variable}/${variable}_${year}_h${h}v${v}.zip</a><br></div>`;
				$(`#dynamic_${variable}`).html(dyn_link);
			}
		};
		console.log("DEBUG: set_paths_landcover defined");
	} catch (e) {
		console.error("Error defining set_paths_landcover:", e);
	}

	try {
		console.log("DEBUG: Defining set_paths...");
		function set_paths(h,v) {

			$("#dynamic_tile_code").attr("h", h);
			$("#dynamic_tile_code").attr("v", v);

			h = String("00" + h).slice(-2);
			v = String("00" + v).slice(-2);
			console.log(`DEBUG: Setting all tile links for h${h}v${v}...`);

			tile_code =
			`<div>
				<p><br><b>
				&nbsp&nbsp&nbsp&nbsp&nbsp
				Tile id: h${h}v${v}</b></p>
			</div>`;
			$("#dynamic_tile_code").html(tile_code);

			url_public = "https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ/download?path=%2F";
			var category = "placeholder";
			var vars = ["placeholder"];

			let selected_button = document.querySelector('input[name="landcover_year"]:checked');
			let year = selected_button ? selected_button.value : "1992";
			set_paths_landcover(h, v, year);

			selected_button1 = document.querySelector('input[name="bioclim_subcat"]:checked');
			selected_button2 = document.querySelector('input[name="bioclim_model"]:checked');
			selected_button3 = document.querySelector('input[name="bioclim_scenario"]:checked');
			let time_period = selected_button1 ? selected_button1.value : "1981-2010_observed";
			let model = selected_button2 ? selected_button2.value : "ipsl-cm6a-lr";
			let scenario = selected_button3 ? selected_button3.value : "ssp126";
			set_paths_bioclim(h, v, time_period, model, scenario);

			category = "hydrography90m_v1_0";
			console.log(`DEBUG: Setting tile links for "${category}"...`);
			vars = ["channel_curv_cel", "channel_dist_dw_seg", "channel_dist_up_cel", "channel_dist_up_seg",
					  "channel_elv_dw_cel", "channel_elv_dw_seg", "channel_elv_up_cel", "channel_elv_up_seg",
					  "channel_grad_dw_seg", "channel_grad_up_cel", "channel_grad_up_seg", "connections",
					  "cti", "cum_length", "elev_drop", "accumulation", "gradient", "length",
					  "out_dist", "out_drop", "outlet_diff_dw_basin", "outlet_diff_dw_scatch", "outlet_dist_dw_basin",
					  "outlet_dist_dw_scatch", "outlet_elev", "sinosoid", "slope_curv_max_dw_cel", "slope_curv_min_dw_cel",
					  "slope_elv_dw_cel", "slope_grad_dw_cel", "source_elev", "spi", "sti", "stream_diff_dw_near",
					  "stream_diff_up_farth", "stream_diff_up_near", "stream_dist_dw_near", "stream_dist_proximity",
					  "stream_dist_up_farth", "stream_dist_up_near", "order_drwal", "order_hack", "order_horton",
					  "order_scheidegger", "order_shreve", "order_strahler", "order_topo", "order_topo_dim", "stright"];
			for (var i = 0; i < vars.length; i++) {
				var variable = vars[i];
				var dyn_link =`<div>Download tile h${h}v${v} here: <br>
					<a href="${url_public}${category}/${variable}/${variable}_h${h}v${v}.zip" target="_blank">
					${url_public}${category}/${variable}/${variable}_h${h}v${v}.zip</a><br></div>`;
				$(`#dynamic_${variable}`).html(dyn_link);
			}

			category = "soilgrids250m_v2_0";
			console.log(`DEBUG: Setting tile links for "${category}"...`);
			vars = ["acdwrb", "awcts", "bdricm", "brdlog", "bldfie", "cecsol", "clyppt", "crfvol",
					  "histpr", "orcdrc", "phihox", "slgwrb", "sltppt", "sndppt", "texmht", "wwp"];
			for (var i = 0; i < vars.length; i++) {
				variable = vars[i];
				dyn_link =`<div>Download tile h${h}v${v} here: <br>
					<a href="${url_public}${category}/${variable}/${variable}_h${h}v${v}.zip">
					${url_public}${category}/${variable}/${variable}_h${h}v${v}.zip</a><br></div>`;
				$(`#dynamic_${variable}`).html(dyn_link);
			}

			category = "cgiar_csi_v3";
			console.log(`DEBUG: Setting tile links for "${category}"...`);
			vars = ["garid", "devapt"];
			for (var i = 0; i < vars.length; i++) {
				variable = vars[i];
				dyn_link =`<div>Download tile h${h}v${v} here: <br>
					<a href="${url_public}${category}/${variable}/${variable}_h${h}v${v}.zip">
					${url_public}${category}/${variable}/${variable}_h${h}v${v}.zip</a><br></div>`;
				$(`#dynamic_${variable}`).html(dyn_link);
			}

			category = "flo1k_v1_0";
			console.log(`DEBUG: Setting tile links for "${category}"...`);
			variable = "flo1k";
			dyn_link =`<div>Download tile h${h}v${v} here: <br>
			<a href="${url_public}${category}/${variable}_h${h}v${v}.zip">
				${url_public}${category}/${variable}_h${h}v${v}.zip</a><br></div>`;
			$(`#dynamic_${variable}`).html(dyn_link);

			category = "merit_dem_v1_0_3";
			console.log(`DEBUG: Setting tile links for "${category}"...`);
			variable = "elev";
			dyn_link =`<div>Download tile h${h}v${v} here: <br>
			<a href="${url_public}${category}/${variable}_h${h}v${v}.zip">
				${url_public}${category}/${variable}_h${h}v${v}.zip</a><br></div>`;
			$(`#dynamic_merit`).html(dyn_link);

			let tile_in_r_example = `h${h}v${v}`;
			console.log("Replacing tiles in R code examples...", tile_in_r_example);
			const r_examples = document.getElementsByClassName('codeblock');
			const regex = /h\d{2}v\d{2}/g;
			for (let el of r_examples) {
				el.innerHTML = el.innerHTML.replace(regex, tile_in_r_example);
			};
		};
		console.log("DEBUG: set_paths defined");
	} catch (e) {
		console.error("Error defining set_paths:", e);
	}
	$(function() {
		$(".tile").on("click", function() {
			$(".tile").removeClass("selected");
			$(this).addClass("selected");
		});
	});
} catch (e) {
	console.error("Fatal error in script:", e);
}
</script>


------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# <a href="/environment90m/environment90m_layers#tile-map">Pick a tile!</a>

... to generate download links.

If you click on any tile, the sections below will feature <b>download links and R code</b> for that specific tile!

<!-- Here the map is defined, each tile individually, and click-handlers are added to
each tile that then call set_paths with that tile's h and v value! -->
<div class="mapTileDownloadContainer">
	<div class="mapTileDownloadBaseLayer"><img width="750" height="300" src="../../images/hydrography90m/basins_noTiles.png" /></div>
	<!-- Row 0 -->
	<div class="tile" style="left:36px;top:32px" title="h00v00" onclick="set_paths(00,00)"></div>
	<div class="tile" style="left:70px;top:32px;width:35px" title="h02v00" onclick="set_paths(02,00)"></div>
	<div class="tile" style="left:104px;top:32px" title="h04v00" onclick="set_paths(04,00)"></div>
	<div class="tile" style="left:138px;top:32px" title="h06v00" onclick="set_paths(06,00)"></div>
	<div class="tile" style="left:172px;top:32px" title="h08v00" onclick="set_paths(08,00)"></div>
	<div class="tile" style="left:206px;top:32px" title="h10v00" onclick="set_paths(10,00)"></div>
	<div class="tile" style="left:240px;top:32px" title="h12v00" onclick="set_paths(12,00)"></div>
	<div class="tile" style="left:274px;top:32px" title="h14v00" onclick="set_paths(14,00)"></div>
	<div class="tile" style="left:308px;top:32px" title="h16v00" onclick="set_paths(16,00)"></div>
	<div class="tile" style="left:342px;top:32px" title="h18v00" onclick="set_paths(18,00)"></div>
	<div class="tile" style="left:376px;top:32px" title="h20v00" onclick="set_paths(20,00)"></div>
	<div class="tile" style="left:410px;top:32px" title="h22v00" onclick="set_paths(22,00)"></div>
	<div class="tile" style="left:444px;top:32px" title="h24v00" onclick="set_paths(24,00)"></div>
	<div class="tile" style="left:478px;top:32px" title="h26v00" onclick="set_paths(26,00)"></div>
	<div class="tile" style="left:512px;top:32px" title="h28v00" onclick="set_paths(28,00)"></div>
	<div class="tile" style="left:546px;top:32px" title="h30v00" onclick="set_paths(30,00)"></div>
	<div class="tile" style="left:580px;top:32px" title="h32v00" onclick="set_paths(32,00)"></div>
	<div class="tile" style="left:614px;top:32px;width:49px" title="h34v00" onclick="set_paths(34,00)"></div>
	<!-- Row 1 -->
	<div class="tile" style="left:36px;top:66px" title="h00v02" onclick="set_paths(00,02)"></div>
	<div class="tile" style="left:70px;top:66px;width:35px" title="h02v02" onclick="set_paths(02,02)"></div>
	<div class="tile" style="left:104px;top:66px" title="h04v02" onclick="set_paths(04,02)"></div>
	<div class="tile" style="left:138px;top:66px" title="h06v02" onclick="set_paths(06,02)"></div>
	<div class="tile" style="left:172px;top:66px" title="h08v02" onclick="set_paths(08,02)"></div>
	<div class="tile" style="left:206px;top:66px" title="h10v02" onclick="set_paths(10,02)"></div>
	<div class="tile" style="left:240px;top:66px" title="h12v02" onclick="set_paths(12,02)"></div>
	<div class="tile" style="left:274px;top:66px" title="h14v02" onclick="set_paths(14,02)"></div>
	<div class="tile" style="left:308px;top:66px" title="h16v02" onclick="set_paths(16,02)"></div>
	<div class="tile" style="left:342px;top:66px" title="h18v02" onclick="set_paths(18,02)"></div>
	<div class="tile" style="left:376px;top:66px" title="h20v02" onclick="set_paths(20,02)"></div>
	<div class="tile" style="left:410px;top:66px" title="h22v02" onclick="set_paths(22,02)"></div>
	<div class="tile" style="left:444px;top:66px" title="h24v02" onclick="set_paths(24,02)"></div>
	<div class="tile" style="left:478px;top:66px" title="h26v02" onclick="set_paths(26,02)"></div>
	<div class="tile" style="left:512px;top:66px" title="h28v02" onclick="set_paths(28,02)"></div>
	<div class="tile" style="left:546px;top:66px" title="h30v02" onclick="set_paths(30,02)"></div>
	<div class="tile" style="left:580px;top:66px" title="h32v02" onclick="set_paths(32,02)"></div>
	<div class="tile" style="left:614px;top:66px;width:49px" title="h34v02" onclick="set_paths(34,02)"></div>
	<!-- Row 2 -->
	<div class="tile" style="left:36px;top:100px" title="h00v04" onclick="set_paths(00,04)"></div>
	<div class="tile" style="left:104px;top:100px" title="h04v04" onclick="set_paths(04,04)"></div>
	<div class="tile" style="left:138px;top:100px" title="h06v04" onclick="set_paths(06,04)"></div>
	<div class="tile" style="left:172px;top:100px" title="h08v04" onclick="set_paths(08,04)"></div>
	<div class="tile" style="left:206px;top:100px" title="h10v04" onclick="set_paths(10,04)"></div>
	<div class="tile" style="left:240px;top:100px" title="h12v04" onclick="set_paths(12,04)"></div>
	<div class="tile" style="left:274px;top:100px" title="h14v04" onclick="set_paths(14,04)"></div>
	<div class="tile" style="left:308px;top:100px" title="h16v04" onclick="set_paths(16,04)"></div>
	<div class="tile" style="left:342px;top:100px" title="h18v04" onclick="set_paths(18,04)"></div>
	<div class="tile" style="left:376px;top:100px" title="h20v04" onclick="set_paths(20,04)"></div>
	<div class="tile" style="left:410px;top:100px" title="h22v04" onclick="set_paths(22,04)"></div>
	<div class="tile" style="left:444px;top:100px" title="h24v04" onclick="set_paths(24,04)"></div>
	<div class="tile" style="left:478px;top:100px" title="h26v04" onclick="set_paths(26,04)"></div>
	<div class="tile" style="left:512px;top:100px" title="h28v04" onclick="set_paths(28,04)"></div>
	<div class="tile" style="left:546px;top:100px" title="h30v04E" onclick="set_paths(30,04)"></div>
	<div class="tile" style="left:580px;top:100px" title="h32v04" onclick="set_paths(32,04)"></div>
	<!-- Row 3 -->
	<div class="tile" style="left:36px;top:134px" title="h00v06" onclick="set_paths(00,06)"></div>
	<div class="tile" style="left:70px;top:134px;width:35px" title="h02v06" onclick="set_paths(02,06)"></div>
	<div class="tile" style="left:138px;top:134px" title="h06v06" onclick="set_paths(06,06)"></div>
	<div class="tile" style="left:172px;top:134px" title="h08v06" onclick="set_paths(08,06)"></div>
	<div class="tile" style="left:206px;top:134px" title="h10v06" onclick="set_paths(10,06)"></div>
	<div class="tile" style="left:240px;top:134px" title="h12v06" onclick="set_paths(12,06)"></div>
	<div class="tile" style="left:274px;top:134px" title="h14v06" onclick="set_paths(14,06)"></div>
	<div class="tile" style="left:308px;top:134px" title="h16v06" onclick="set_paths(16,06)"></div>
	<div class="tile" style="left:342px;top:134px" title="h18v06" onclick="set_paths(18,06)"></div>
	<div class="tile" style="left:376px;top:134px" title="h20v06" onclick="set_paths(20,06)"></div>
	<div class="tile" style="left:410px;top:134px" title="h22v06" onclick="set_paths(22,06)"></div>
	<div class="tile" style="left:444px;top:134px" title="h24v06" onclick="set_paths(24,06)"></div>
	<div class="tile" style="left:478px;top:134px" title="h26v06" onclick="set_paths(26,06)"></div>
	<div class="tile" style="left:512px;top:134px" title="h28v06" onclick="set_paths(28,06)"></div>
	<div class="tile" style="left:546px;top:134px" title="h30v06" onclick="set_paths(30,06)"></div>
	<div class="tile" style="left:580px;top:134px" title="h32v06" onclick="set_paths(32,06)"></div>
	<div class="tile" style="left:614px;top:134px;width:33px" title="h34v06" onclick="set_paths(34,06)"></div>
	<!-- Row 4 -->
	<div class="tile" style="left:36px;top:168px" title="h00v08" onclick="set_paths(00,08)"></div>
	<div class="tile" style="left:70px;top:168px;width:35px" title="h02v08" onclick="set_paths(02,08)"></div>
	<div class="tile" style="left:104px;top:168px" title="h04v08" onclick="set_paths(04,08)"></div>
	<div class="tile" style="left:172px;top:168px" title="h08v08" onclick="set_paths(08,08)"></div>
	<div class="tile" style="left:206px;top:168px" title="h10v08" onclick="set_paths(10,08)"></div>
	<div class="tile" style="left:240px;top:168px" title="h12v08" onclick="set_paths(12,08)"></div>
	<div class="tile" style="left:274px;top:168px" title="h14v08" onclick="set_paths(14,08)"></div>
	<div class="tile" style="left:308px;top:168px" title="h16v08" onclick="set_paths(16,08)"></div>
	<div class="tile" style="left:342px;top:168px" title="h18v08" onclick="set_paths(18,08)"></div>
	<div class="tile" style="left:376px;top:168px" title="h20v08" onclick="set_paths(20,08)"></div>
	<div class="tile" style="left:410px;top:168px" title="h22v08" onclick="set_paths(22,08)"></div>
	<div class="tile" style="left:444px;top:168px" title="h24v08" onclick="set_paths(24,08)"></div>
	<div class="tile" style="left:478px;top:168px" title="h26v08" onclick="set_paths(26,08)"></div>
	<div class="tile" style="left:512px;top:168px" title="h28v08" onclick="set_paths(28,08)"></div>
	<div class="tile" style="left:546px;top:168px" title="h30v08" onclick="set_paths(30,08)"></div>
	<div class="tile" style="left:580px;top:168px" title="h32v08" onclick="set_paths(32,08)"></div>
	<div class="tile" style="left:614px;top:168px;width:33px" title="h34v08" onclick="set_paths(34,08)"></div>
	<!-- Row 5 -->
	<div class="tile" style="left:36px;top:202px" title="h00v10" onclick="set_paths(00,10)"></div>
	<div class="tile" style="left:70px;top:202px;width:35px" title="h02v10" onclick="set_paths(02,10)"></div>
	<div class="tile" style="left:104px;top:202px" title="h04v10" onclick="set_paths(04,10)"></div>
	<div class="tile" style="left:138px;top:202px" title="h06v10" onclick="set_paths(06,10)"></div>
	<div class="tile" style="left:172px;top:202px" title="h08v10" onclick="set_paths(08,10)"></div>
	<div class="tile" style="left:206px;top:202px" title="h10v10" onclick="set_paths(10,10)"></div>
	<div class="tile" style="left:240px;top:202px" title="h12v10" onclick="set_paths(12,10)"></div>
	<div class="tile" style="left:274px;top:202px" title="h14v10" onclick="set_paths(14,10)"></div>
	<div class="tile" style="left:308px;top:202px" title="h16v10" onclick="set_paths(16,10)"></div>
	<div class="tile" style="left:342px;top:202px" title="h18v10" onclick="set_paths(18,10)"></div>
	<div class="tile" style="left:376px;top:202px" title="h20v10" onclick="set_paths(20,10)"></div>
	<div class="tile" style="left:410px;top:202px" title="h22v10" onclick="set_paths(22,10)"></div>
	<div class="tile" style="left:444px;top:202px" title="h24v10" onclick="set_paths(24,10)"></div>
	<div class="tile" style="left:512px;top:202px" title="h28v10" onclick="set_paths(28,10)"></div>
	<div class="tile" style="left:546px;top:202px" title="h30v10" onclick="set_paths(30,10)"></div>
	<div class="tile" style="left:580px;top:202px" title="h32v10" onclick="set_paths(32,10)"></div>
	<div class="tile" style="left:614px;top:202px;width:33px" title="h34v10" onclick="set_paths(34,10)"></div>
	<!-- Row 6 -->
	<div class="tile" style="left:36px;top:236px;height:42px" title="h00v12" onclick="set_paths(00,12)"></div>
	<div class="tile" style="left:206px;top:236px;height:42px" title="h10v12" onclick="set_paths(10,12)"></div>
	<div class="tile" style="left:240px;top:236px;height:42px" title="h12v12" onclick="set_paths(12,12)"></div>
	<div class="tile" style="left:274px;top:236px;height:42px" title="h14v12" onclick="set_paths(14,12)"></div>
	<div class="tile" style="left:308px;top:236px;height:42px" title="h16v12" onclick="set_paths(16,12)"></div>
	<div class="tile" style="left:342px;top:236px;height:42px" title="h18v12" onclick="set_paths(18,12)"></div>
	<div class="tile" style="left:376px;top:236px;height:42px" title="h20v12" onclick="set_paths(20,12)"></div>
	<div class="tile" style="left:410px;top:236px;height:42px" title="h22v12" onclick="set_paths(22,12)"></div>
	<div class="tile" style="left:444px;top:236px;height:42px" title="h24v12" onclick="set_paths(24,12)"></div>
	<div class="tile" style="left:512px;top:236px;height:42px" title="h28v12" onclick="set_paths(28,12)"></div>
	<div class="tile" style="left:546px;top:236px;height:42px" title="h30v12" onclick="set_paths(30,12)"></div>
	<div class="tile" style="left:580px;top:236px;height:42px" title="h32v12" onclick="set_paths(32,12)"></div>
	<div class="tile" style="left:614px;top:236px;width:33px;height:42px" title="h34v12" onclick="set_paths(34,02)"></div>
</div>
<div id="tilepaths"></div>
<div id="dynamic_tile_code" h="999" v=999><p><br><b><span style="color:lightgrey">(No tile selected yet)</span></b></p></div>

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<div id="esa" class="anchorcontainer"></div><br>
# <a href="/environment90m/environment90m_layers#esa">Land Cover (ESA-CCI)</a>
<a href="#top-of-page">Back to top</a> &nbsp; <a href="#chelsa">Next category</a><br>

For land use data, we aggregated the consistent global land cover maps of the <em>Land Cover European Space Agency (ESA) Climate Change Initiative (CCI)</em> project into 22 categories from the original 37 ESA category level 2 land cover classes at a spatial resolution of 300m (<em>CCI (2017)</em>, see <a href="#references">references</a> below). The annual data are available for the years 1992 to 2020. The data source is ESA (2017) (see <a href="#references">references</a> below).

* How to <a href="https://glowabio.github.io/hydrographr/reference/download_env90m_tables.html" target="_blank">download the data</a> using the R package <a href="https://glowabio.github.io/hydrographr/" target="_blank">hydrographr</a>:

<span class="codeblock" id="codeblock_landcover">
download_landcover_tables(<br>
base_vars=c("c10", "c130"),
years=c(1992),
tile_ids=c("h00v04"),
download_dir=".",
download=TRUE)
</span>

* Directory containing all the variables: <a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fesa_cci_landcover_v2_1_1" target="_blank">public.igb-berlin.de</a>

* Pick a year to generate download links for all land cover variables for that year:

<div class="radio-buttons">
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="1992">1992</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="1993">1993</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="1994">1994</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="1995">1995</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="1996">1996</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="1997">1997</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="1998">1998</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="1999">1999</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2000">2000</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2001">2001</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2002">2002</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2003">2003</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2004">2004</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2005">2005</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2006">2006</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2007">2007</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2008">2008</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2009">2009</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2010">2010</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2011">2011</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2012">2012</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2013">2013</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2014">2014</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2015">2015</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2016">2016</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2017">2017</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2018">2018</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2018">2019</label>
	<label class="landcover-year-label"><input name="landcover_year" type="radio" value="2018">2020</label>
</div>

<!-- Define click handler for Landcover radio-buttons (year) -->
<script>
	try {
	console.log("DEBUG: Defining click handler for year buttons...");
	const radios_landcover = document.querySelectorAll('input[name="landcover_year"]');
	radios_landcover.forEach(radio => {
		radio.addEventListener('change', () => {

			let selectedOption = document.querySelector('input[name="landcover_year"]:checked').value;
			console.log(`DEBUG: Selected year: ${selectedOption}`);

			let h = parseInt($("#dynamic_tile_code").attr("h"));
			let v = parseInt($("#dynamic_tile_code").attr("v"));
			if (h>90) alert("Please don't forgot to select a tile on the map above to get functioning download links.");
			set_paths_landcover(h, v, selectedOption);

			radios_landcover.forEach(radiobutton => radiobutton.classList.remove('selected'));
			const labels_landcover = document.querySelectorAll('.landcover-year-label');
			labels_landcover.forEach(lab => lab.classList.remove('selected'));

			radio.classList.add('selected');
			radio.parentElement.classList.add('selected');

			console.log("Replacing year in R code examples...", selectedOption);
			const el = document.getElementById('codeblock_landcover');
			const regex = /c\(\d{4}\)/g;
			el.innerHTML = el.innerHTML.replace(regex, "c("+selectedOption+")");
		});
	});
} catch (e) {
	console.error("Fatal error in script:", e);
}
</script>

<!-- Table containing Landcover variables -->
<table style="width:100%; background-image:none">
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c10"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c10">c10: Cropland, rainfed</a></th>
	</tr>
	<tr>
		<td>Cropland, rainfed. Combined classes 10+11+12.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<tr>
		<td><div id="dynamic_c10"><span style="color:lightgrey">Download link for selectedd tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c20"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c20">c20: Cropland, irrigated/post-flooding</a></th>
	</tr>
	<tr>
		<td>Cropland, irrigated or post-flooding.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<embed src="/images/environment90m/layer_images/fake_placeholder.png" alt="c20_<year>_*.txt" width="320"/>
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fr.watershed%2Fdirection_tiles20d" target="_blank"> direction_*.tif (raster)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_direction_cog&view=True" target="_blank">[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c20"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c30"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c30">c30: Cropland/natural vegetation</a></th>
	</tr>
	<tr>
		<td>Mosaic cropland (>50%) - natural vegetation (tree, shrub, herbaceous cover) (<50%).</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<embed src="/images/environment90m/layer_images/fake_placeholder.png" alt="c30_<year>_*.txt" width="320"/>
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fr.watershed%2Fdirection_tiles20d" target="_blank"> direction_*.tif (raster)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_direction_cog&view=True" target="_blank">[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c30"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c40"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c40">c40: Natural vegetation/cropland</a></th>
	</tr>
	<tr>
		<td>Mosaic natural vegetation (tree, shrub, herbaceous cover) (>50%) / cropland (<50%).</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<embed src="/images/environment90m/layer_images/fake_placeholder.png" alt="c40_<year>_*.txt" width="320"/>
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fr.watershed%2Fdirection_tiles20d" target="_blank"> direction_*.tif (raster)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_direction_cog&view=True" target="_blank">[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>	
		<td><div id="dynamic_c40"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c50"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c50">c50: Tree cover, broadleaved, evergreen</a></th>
	</tr>
	<tr>
		<td>Tree cover, broadleaved, evergreen, closed to open (>15%).</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<embed src="/images/environment90m/layer_images/fake_placeholder.png" alt="c50_<year>_*.txt" width="320"/>
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fr.watershed%2Fdirection_tiles20d" target="_blank"> direction_*.tif (raster)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_direction_cog&view=True" target="_blank">[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>	
		<td><div id="dynamic_c50"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c60"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c60">c60: Tree cover, broadleaved, deciduous</a></th>
	</tr>
	<tr>
		<td>Tree cover, broadleaved, deciduous, closed to open (>15%). Combined classes: 60+61+62.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<embed src="/images/environment90m/layer_images/fake_placeholder.png" alt="c60_<year>_*.txt" width="320"/>
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fr.watershed%2Fdirection_tiles20d" target="_blank"> direction_*.tif (raster)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_direction_cog&view=True" target="_blank">[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>	
		<td><div id="dynamic_c60"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c70"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c70">c70: Tree cover, needleleaved, evergreen</a></th>
	</tr>
	<tr>
		<td>Tree cover, needleleaved, evergreen, closed to open (>15%). Combined classes 70+71+72.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<embed src="/images/environment90m/layer_images/fake_placeholder.png" alt="c30_<year>_*.txt" width="320"/>
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fr.watershed%2Fdirection_tiles20d" target="_blank"> direction_*.tif (raster)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_direction_cog&view=True" target="_blank">[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>	
		<td><div id="dynamic_c70"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c80"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c80">c80: Tree cover, needleleaved, deciduous</a></th>
	</tr>
	<tr>
		<td>Tree cover, needleleaved, deciduous, closed to open (>15%). Combined classes 80+81+82.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<embed src="/images/environment90m/layer_images/fake_placeholder.png" alt="c30_<year>_*.txt" width="320"/>
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fr.watershed%2Fdirection_tiles20d" target="_blank"> direction_*.tif (raster)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_direction_cog&view=True" target="_blank">[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>	
		<td><div id="dynamic_c80"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c90"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c90">c90: Tree cover, mixed leaf type</a></th>
	</tr>
	<tr>
		<td>Tree cover, mixed leaf type (broadleaved and needleleaved).</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c90_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c90_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c90"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c100"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c100">c100: Tree and shrub</a></th>
	</tr>
	<tr>
		<td>Mosaic tree and shrub (>50%) / herbaceous cover (<50%).</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c100_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c100_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c100"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c110"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c110">c110: Herbaceous/tree and shrub</a></th>
	</tr>
	<tr>
		<td>Mosaic herbaceous cover (>50%) / tree and shrub (<50%).</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c110_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c110_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c110"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c120"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c120">c120: Shrubland</a></th>
	</tr>
	<tr>
		<td>Shrubland. Combined classes 120+121+122.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c120_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c120_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c120"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c130"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c130">c130: Grassland</a></th>
	</tr>
	<tr>
		<td>Grassland.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c130_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c130_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c130"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c140"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c140">c140: Lichens, mosses</a></th>
	</tr>
	<tr>
		<td>Lichens, mosses.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c140_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c140_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c140"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c150"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c150">c150: Sparse vegetation</a></th>
	</tr>
	<tr>
		<td>Sparse vegetation (tree, shrub, herbaceous cover) (<15%). Combined classes 150+151+152+153.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c150_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c150_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c150"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c160"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c160">c160: Tree cover, flooded, fresh/brackish water</a></th>
	</tr>
	<tr>
		<td>Tree cover, flooded, fresh or brackish water.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c160_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c160_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c160"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c170"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c170">c170: Tree cover, flooded, saline water</a></th>
	</tr>
	<tr>
		<td>Tree cover, flooded, saline water.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c170_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c170_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c170"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c180"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c180">c180: Shrub or herbaceous</a></th>
	</tr>
	<tr>
		<td>Shrub or herbaceous cover, flooded, fresh - saline - brackish water.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c180_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c180_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c180"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c190"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c190">c190: Urban areas</a></th>
	</tr>
	<tr>
		<td>Urban areas.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/esa_cci_landcover_v2_1_1/c190_2000_h18v02_subset_map.png" alt="c190_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c190_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c190"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c200"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c200">c200: Bare areas</a></th>
	</tr>
	<tr>
		<td>Bare areas. Combined classes 200+201+202.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c200_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c200_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c200"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c210"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c210">c210: Water bodies</a></th>
	</tr>
	<tr>
		<td>Water bodies.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c210_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c210_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c210"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="c220"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#c220">c220: Snow and ice</a></th>
	</tr>
	<tr>
		<td>Permanent snow and ice.</td>
	</tr>
	<tr>
		<td>Unit: Proportion</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="c220_<year>*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> c220_year_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_c220"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
</table>


------------------------------------------------------------------------------------------------------------------------------------------------------------------------


<div id="chelsa" class="anchorcontainer"></div><br>
# <a href="/environment90m/environment90m_layers#chelsa">Bioclimatic Variables (CHELSA)</a>
<a href="#top-of-page">Back to top</a> &nbsp; <a href="#soil">Next category</a><br>

We derived high-resolution climate information from the Chelsa v2.1 dataset available at <a href="https://chelsa-climate.org/">chelsa-climate.org</a> (<em>Karger et al. 2017, 2021</em>, see <a href="#references">references</a> below). We used 19 bioclimatic variables (bio 1 to 19) at 30-arc-sec (ca. 1 km²) resolution for 30-year
averages of temperature and precipitation. We aggregated the data for three time ranges: from 1981 to 2010, corresponding to observational data, and future projections for the years 2041 to 2070, as well as 2071 to 2100, corresponding to 2050 and 2070, respectively. For each future projection, we used general circulation models (GCMs) following three shared socioeconomic pathways (SSP1-RCP2.6, SSP3-RCP7, and SSP5-RCP8.5; Ebi et al. (2014); O’Neill et al. (2017), see <a href="#references">references</a> below).

* How to download observed data using the R package <a href="https://glowabio.github.io/hydrographr/">hydrographr</a>:

<span class="codeblock codeblock_bioclim_obs">
download_observed_climate_tables( <br>
subset = c("bio01_1981-2010_observed"),
tile_ids = c("h00v04"),
download = TRUE,
download_dir = ".")
</span>

* How to download projected data using the R package <a href="https://glowabio.github.io/hydrographr/">hydrographr</a>:

<span class="codeblock codeblock_bioclim_proj">
download_projected_climate_tables(<br>
subset = c("bio01_2071-2100_ukesm1-0-ll_ssp585_v2_1"),
tile_ids = c("h00v04"),
download_dir = ".",
download = TRUE)
</span>

You can also specify the separate aspects separately (time period, scenario, ...):

<span class="codeblock codeblock_bioclim_proj">
download_projected_climate_tables(<br>
base_vars = c("bio01"),
time_periods = c("2071-2100"),
models=c("ukesm1-0-ll"),
scenarios=c("ssp585"),
version=c("v2_1"),
tile_ids = c("h00v04"),
download = TRUE)
</span>


* Directory containing all the variables: <a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fchelsa_bioclim_v2_1" target="_blank">public.igb-berlin.de</a>

* Pick a time period to generate download links for all bioclim variables for that period:
<div class="radio-buttons">
	<label class="bioclim-subcat-label"><input name="bioclim_subcat" type="radio" value="1981-2010_observed" >1981-2010_observed</label>
	<label class="bioclim-subcat-label"><input name="bioclim_subcat" type="radio" value="2041-2070_projected">2041-2070_projected</label>
	<label class="bioclim-subcat-label"><input name="bioclim_subcat" type="radio" value="2071-2100_projected">2071-2100_projected</label>
</div>

* Pick a model to generate download links for all bioclim variables for that model:

<div class="radio-buttons">
	<label class="bioclim-model-label"><input name="bioclim_model" type="radio" value="ipsl-cm6a-lr" >ipsl-cm6a-lr</label>
	<label class="bioclim-model-label"><input name="bioclim_model" type="radio" value="mpi-esm1-2-hr">mpi-esm1-2-hr</label>
	<label class="bioclim-model-label"><input name="bioclim_model" type="radio" value="ukesm1-0-ll"  >ukesm1-0-ll</label>
</div>

* Pick a scenario to generate download links for all bioclim variables for that scenario:

<div class="radio-buttons">
	<label class="bioclim-scenario-label"><input name="bioclim_scenario" type="radio" value="ssp126">ssp126</label>
	<label class="bioclim-scenario-label"><input name="bioclim_scenario" type="radio" value="ssp370">ssp370</label>
	<label class="bioclim-scenario-label"><input name="bioclim_scenario" type="radio" value="ssp585">ssp585</label>
</div>


<!-- Define click handlers for Bioclim radio-buttons (model, scenario, time period) -->
<script>
	try {

	console.log("DEBUG: Defining click handler for bioclim time period buttons...");
	const radios_bioclim = document.querySelectorAll('input[name="bioclim_subcat"]');
	radios_bioclim.forEach(radio => {
		radio.addEventListener('change', () => {

			/* Get values for time period, model and scenario. */
			/* Use defaults if user did not specify any. */
			/* Note: "model" and "scenario" are irrelevant if user selects "observed", */
			/* they are ignored in function "set_paths_bioclim()". */
			selected_button1 = document.querySelector('input[name="bioclim_subcat"]:checked');
			selected_button2 = document.querySelector('input[name="bioclim_model"]:checked');
			selected_button3 = document.querySelector('input[name="bioclim_scenario"]:checked');
			let time_period = selected_button1 ? selected_button1.value : "1981-2010_observed";
			let model = selected_button2 ? selected_button2.value : "ipsl-cm6a-lr";
			let scenario = selected_button3 ? selected_button3.value : "ssp126";
			console.log(`DEBUG: Selected time_period: ${time_period}`);

			/* Get tile that was selected by user: */
			let h = parseInt($("#dynamic_tile_code").attr("h"));
			let v = parseInt($("#dynamic_tile_code").attr("v"));
			if (h>90) alert("Please don't forgot to select a tile on the map above to get functioning download links.");
			set_paths_bioclim(h, v, time_period, model, scenario);

			/* Unselect the other buttons */
			radios_bioclim.forEach(radioo => {
				radioo.checked = false;
				radioo.classList.remove('selected');
				radioo.closest('label')?.classList.remove('selected');
			});

			/* Select the selected one: */
			radio.checked = true;
			radio.classList.add('selected');
			radio.parentElement.classList.add('selected');

			/* If the time period "observed" was selected, grey out the model and scenario buttons, */
			/* and remove the grey-out once a "projected" time period is selected! */
			/* Do not touch whether they are "checked" or not - so that the "checkedness" */
			/* (r.checked = true;) is kept and stays until the greying-out is undone! */
			if (time_period === "1981-2010_observed") {
				console.log('Greying out...');
				let modelRadios = document.querySelectorAll('input[name="bioclim_model"]');
				modelRadios.forEach(r => {
					r.disabled = true;
					r.closest('label')?.classList.toggle('disabled', true);
				});
				let scenarioRadios = document.querySelectorAll('input[name="bioclim_scenario"]');
				scenarioRadios.forEach(r => {
					r.disabled = true;
					r.closest('label')?.classList.toggle('disabled', true);
				});
			} else {
				console.log('Undoing grey-out...');
				let modelRadios = document.querySelectorAll('input[name="bioclim_model"]');
				modelRadios.forEach(r => {
					r.disabled = false;
					r.closest('label')?.classList.toggle('disabled', false);
				});
				let scenarioRadios = document.querySelectorAll('input[name="bioclim_scenario"]');
				scenarioRadios.forEach(r => {
					r.disabled = false;
					r.closest('label')?.classList.toggle('disabled', false);
				});
			}

			/* Replace time_period in R code: */
			console.log("Replacing time_period in R code examples...", time_period);
			if (time_period.endsWith("_projected")) {
				const elements = document.getElementsByClassName('codeblock_bioclim_proj');
				for (let el of elements) {
					el.innerHTML = el.innerHTML.replace("2041-2070_projected", time_period);
					el.innerHTML = el.innerHTML.replace("2071-2100_projected", time_period);
					let time_period_only = time_period.replace('_projected','').replace('_observed','');
					el.innerHTML = el.innerHTML.replace("2041-2070", time_period_only);
					el.innerHTML = el.innerHTML.replace("2071-2100", time_period_only);
				};
			};
		});
	});

	console.log("DEBUG: Defining click handler for bioclim model buttons...");
	const radios_bioclim2 = document.querySelectorAll('input[name="bioclim_model"]');
	radios_bioclim2.forEach(radio => {
		radio.addEventListener('change', () => {

			/* Get values for time period, model and scenario. */
			/* Use defaults if user did not specify any. */
			/* Note: "model" and "scenario" are irrelevant if user has selected "observed", */
			/* they are ignored in function "set_paths_bioclim()". */
			selected_button1 = document.querySelector('input[name="bioclim_subcat"]:checked');
			selected_button2 = document.querySelector('input[name="bioclim_model"]:checked');
			selected_button3 = document.querySelector('input[name="bioclim_scenario"]:checked');
			let time_period = selected_button1 ? selected_button1.value : "1981-2010_observed";
			let model = selected_button2 ? selected_button2.value : "ipsl-cm6a-lr";
			let scenario = selected_button3 ? selected_button3.value : "ssp126";
			console.log(`DEBUG: Selected model: ${model}`);

			/* Get tile that was selected by user: */
			let h = parseInt($("#dynamic_tile_code").attr("h"));
			let v = parseInt($("#dynamic_tile_code").attr("v"));
			if (h>90) alert("Please don't forgot to select a tile on the map above to get functioning download links.");
			set_paths_bioclim(h, v, time_period, model, scenario);

			/* Unselect the other buttons */
			radios_bioclim2.forEach(radioo => {
				radioo.checked = false;
				radioo.classList.remove('selected');
				radioo.closest('label')?.classList.remove('selected');
			});

			/* Select the selected one: */
			radio.checked = true;
			radio.classList.add('selected');
			radio.parentElement.classList.add('selected');

			/* Replace model in R code: */
			console.log("Replacing model in R code examples...", model);
			const elements = document.getElementsByClassName('codeblock_bioclim_proj');
			const regex = /(ipsl-cm6a-lr|mpi-esm1-2-hr|ukesm1-0-ll)/gi;
			for (let el of elements) {
				el.innerHTML = el.innerHTML.replace(regex, model);
			};
		});
	});

	console.log("DEBUG: Defining click handler for bioclim scenario buttons...");
	const radios_bioclim3 = document.querySelectorAll('input[name="bioclim_scenario"]');
	radios_bioclim3.forEach(radio => {
		radio.addEventListener('change', () => {

			/* Get values for time period, model and scenario. */
			/* Use defaults if user did not specify any. */
			/* Note: "model" and "scenario" are irrelevant if user has selected "observed", */
			/* they are ignored in function "set_paths_bioclim()". */
			selected_button1 = document.querySelector('input[name="bioclim_subcat"]:checked');
			selected_button2 = document.querySelector('input[name="bioclim_model"]:checked');
			selected_button3 = document.querySelector('input[name="bioclim_scenario"]:checked');
			let time_period = selected_button1 ? selected_button1.value : "1981-2010_observed";
			let model = selected_button2 ? selected_button2.value : "ipsl-cm6a-lr";
			let scenario = selected_button3 ? selected_button3.value : "ssp126";
			console.log(`DEBUG: Selected scenario: ${scenario}`);

			/* Get tile that was selected by user: */
			let h = parseInt($("#dynamic_tile_code").attr("h"));
			let v = parseInt($("#dynamic_tile_code").attr("v"));
			if (h>90) alert("Please don't forgot to select a tile on the map above to get functioning download links.");
			set_paths_bioclim(h, v, time_period, model, scenario);

			/* Unselect the other buttons */
			radios_bioclim3.forEach(radioo => {
				radioo.checked = false;
				radioo.classList.remove('selected');
				radioo.closest('label')?.classList.remove('selected');
			});

			/* Select the selected one: */
			radio.checked = true;
			radio.classList.add('selected');
			radio.parentElement.classList.add('selected');

			/* Replace scenario in R code: */
			console.log("Replacing scenario in R code examples...", model);
			const elements = document.getElementsByClassName('codeblock_bioclim_proj');
			const regex = /ssp\d{3}/g;
			for (let el of elements) {
				el.innerHTML = el.innerHTML.replace(regex, scenario);
			};
		});
	});
} catch (e) {
	console.error("Fatal error in script:", e);
}
</script>

<!-- Table containing BioClim variables -->
<table style="width:100%; background-image:none">
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio01"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio01">bio01: Annual mean temperature</a></th>
	</tr>
	<tr>
		<td>Mean annual daily mean air temperatures averaged over 1 year.</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -273.15</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio01_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio01_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio01"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio02"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio02">bio02: Mean diurnal range</a></th>
	</tr>
	<tr>
		<td>Mean diurnal range of temperatures averaged over 1 year.</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio02_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio02_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio02"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio03"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio03">bio03: Isothermality</a></th>
	</tr>
	<tr>
		<td>Ratio of diurnal variation to annual variation in temperatures.</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio03_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio03_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio03"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio04"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio04">bio04: Temperature seasonality</a></th>
	</tr>
	<tr>
		<td>Standard deviation of the monthly mean temperatures.</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius / 100<br>Scale: 0.1<br>Offset: None.</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio04_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio04_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio04"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio05"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio05">bio05: Max temperature of warmest month</a></th>
	</tr>
	<tr>
		<td>The highest temperature of any monthly daily mean maximum temperature.</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -273.15</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/chelsa_bioclim_v2_1/bio5_h18v02_subset_map.png" alt="bio05_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio05_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio05"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio06"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio06">bio06: Min temperature of coldest month</a></th>
	</tr>
	<tr>
		<td>The lowest temperature of any monthly daily mean minimum temperature.</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -273.15</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio06_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio06_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio06"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio07"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio07">bio07: Temperature annual range</a></th>
	</tr>
	<tr>
		<td>The difference between the Maximum Temperature of Warmest month and the Minimum Temperature of Coldest month.</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio07_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio07_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio07"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio08"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio08">bio08: Mean temperature of wettest quarter</a></th>
	</tr>
	<tr>
		<td>The wettest quarter of the year is determined (to the nearest month).</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -273.15</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio08_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio08_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio08"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio09"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio09">bio09: Mean temperature of driest quarter</a></th>
	</tr>
	<tr>
		<td>The driest quarter of the year is determined (to the nearest month).</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -273.15</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio09_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio09_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio09"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio10"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio10">bio10: Mean temperature of warmest quarter</a></th>
	</tr>
	<tr>
		<td>The warmest quarter of the year is determined (to the nearest month).</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -273.15</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio10_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio10_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio10"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio11"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio11">bio11: Mean temperature of coldest quarter</a></th>
	</tr>
	<tr>
		<td>The coldest quarter of the year is determined (to the nearest month).</td>
	</tr>
	<tr>
		<td>Unit: Degrees Celsius<br>Scale: 0.1<br>Offset: -273.15</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio11_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio11_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio11"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio12"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio12">bio12: Annual precipitation</a></th>
	</tr>
	<tr>
		<td>Accumulated precipitation amount over 1 year.</td>
	</tr>
	<tr>
		<td>Unit: kg/m²<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio12_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio12_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio12"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio13"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio13">bio13: Precipitation of wettest month</a></th>
	</tr>
	<tr>
		<td>The precipitation amount of the wettest month.</td>
	</tr>
	<tr>
		<td>Unit: kg/m²<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio13_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio13_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio13"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio14"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio14">bio14: Precipitation of driest month</a></th>
	</tr>
	<tr>
		<td>The precipitation amount of the driest month.</td>
	</tr>
	<tr>
		<td>Unit: kg/m²<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio14_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio14_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio14"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio15"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio15">bio15: Precipitation seasonality</a></th>
	</tr>
	<tr>
		<td>The Coefficient of Variation is the standard deviation of the monthly precipitation estimates expressed as a percentage of the mean of those estimates (i.e. the annual mean).</td>
	</tr>
	<tr>
		<td>Unit: kg/m²<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio15_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio15_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio15"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio16"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio16">bio16: Precipitation of wettest quarter</a></th>
	</tr>
	<tr>
		<td>The wettest quarter of the year is determined (to the nearest month).</td>
	</tr>
	<tr>
		<td>Unit: kg/m²<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio16_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio16_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio16"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio17"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio17">bio17: Precipitation of driest quarter</a></th>
	</tr>
	<tr>
		<td>The driest quarter of the year is determined (to the nearest month).</td>
	</tr>
	<tr>
		<td>Unit: kg/m²<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio17_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio17_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio17"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio18"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio18">bio18: Precipitation of warmest quarter</a></th>
	</tr>
	<tr>
		<td>The warmest quarter of the year is determined (to the nearest month).</td>
	</tr>
	<tr>
		<td>Unit: kg/m²<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio18_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio18_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio18"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bio19"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bio19">bio19: Precipitation of coldest quarter</a></th>
	</tr>
	<tr>
		<td>The coldest quarter of the year is determined (to the nearest month).</td>
	</tr>
	<tr>
		<td>Unit: kg/m²<br>Scale: 0.1<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bio19_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bio19_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bio19"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
</table>

------------------------------------------------------------------------------------------------------------------------------------------------------------------------


<div id="soil" class="anchorcontainer"></div><br>
# <a href="/environment90m/environment90m_layers#soil">Soil (SoilGrids250)</a>
<a href="#top-of-page">Back to top</a> &nbsp; <a href="#flo1k">Next category</a><br>


The soil dataset consists of 16 variables that represent chemical and physical soil properties globally. These variables were sourced from the global gridded soil information dataset, <b>SoilGrids250 v2.0</b>, which is originally provided at seven standard depths for each numerical soil property (with the exception of depth to bedrock and soil organic carbon content) and at a spatial resolution of 250 m (<em>Hengl et al. (2017)</em>, see <a href="#references">references</a> below). To integrate all soil depths (up to 220 cm), we calculated the weighted average for each soil property originally measured at different depths (<em>Hengl et al. (2017)</em>) and finally aggregated the 16 variables across Hydrography90m sub-catchments (<em>Amatulli et al. (2022)</em>, see <a href="#references">references</a> below).


* How to <a href="https://glowabio.github.io/hydrographr/reference/download_env90m_tables.html" target="_blank">download the data</a> using the R package <a href="https://glowabio.github.io/hydrographr/" target="_blank">hydrographr</a>:

<span class="codeblock">
download_soil_tables( <br>
subset = c("clyppt"),
tile_ids = c("h00v04"),
download_dir = ".",
download = TRUE)
</span>


* Directory containing all the variables: <a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fsoilgrids250m_v2_0" target="_blank">public.igb-berlin.de</a><!--a href="https://public.igb-berlin.de/index.php/apps/files?dir=/environment90m_v.1.0/soilgrids250m_v2_0&fileid=1310547" target="_blank">public.igb-berlin.de</a-->


<table style="width:100%; background-image:none">
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="awcts"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#awcts">awcts: Derived saturated water content</a></th>
	</tr>
	<tr>
		<td>Derived saturated water content.</td>
	</tr>
	<tr>
		<td>Unit: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="awcts_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> awcts_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_awcts"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="clyppt"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#clyppt">clyppt: Clay content</a></th>
	</tr>
	<tr>
		<td>Clay content.</td>
	</tr>
	<tr>
		<td>Unit: Percent</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/soilgrids250m_v2_0/clyppt_h18v02_subset_map.png" alt="clyppt_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> clyppt_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_clyppt"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="sndppt"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#sndppt">sndppt: Sand content</a></th>
	</tr>
	<tr>
		<td>Sand content.</td>
	</tr>
	<tr>
		<td>Unit: Percent</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="sndppt_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> sndppt_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_sndppt"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="sltppt"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#sltppt">sltppt: Silt content</a></th>
	</tr>
	<tr>
		<td>Silt content.</td>
	</tr>
	<tr>
		<td>Unit: Percent</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="sltppt_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> sltppt_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_sltppt"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="wwp"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#wwp">wwp: Derived available soil water capacity</a></th>
	</tr>
	<tr>
		<td>Derived available soil water capacity.</td>
	</tr>
	<tr>
		<td>Unit: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="wwp_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> wwp_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_wwp"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="texmht"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#texmht">texmht: Texture class</a></th>
	</tr>
	<tr>
		<td>Texture class. Following the USDA classification.</td>
	</tr>
	<tr>
		<td>Unit: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="texmht_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> texmht_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_texmht"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="orcdrc"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#orcdrc">orcdrc: Soil organic carbon content</a></th>
	</tr>
	<tr>
		<td>Soil organic carbon content.</td>
	</tr>
	<tr>
		<td>Unit: g/kg.</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="orcdrc_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> orcdrc_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_orcdrc"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="phihox"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#phihox">phihox: Soil pH</a></th>
	</tr>
	<tr>
		<td>Soil pH x 10 in H2O.</td>
	</tr>
	<tr>
		<td>Unit: pH</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="phihox_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> phihox_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_phihox"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bldfie"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bldfie">bldfie: Bulk density</a></th>
	</tr>
	<tr>
		<td>Bulk density.</td>
	</tr>
	<tr>
		<td>Unit: Kg/m³</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bldfie_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bldfie_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bldfie"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="cecsol"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#cecsol">cecsol: Cation exchange capacity</a></th>
	</tr>
	<tr>
		<td>Cation exchange capacity.</td>
	</tr>
	<tr>
		<td>Unit: cmolc/kg</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="cecsol_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> cecsol_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_cecsol"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="crfvol"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#crfvol">crfvol: Coarse fragments volumetric</a></th>
	</tr>
	<tr>
		<td>Coarse fragments volumetric.</td>
	</tr>
	<tr>
		<td>Unit: Percent</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="crfvol_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> crfvol_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_crfvol"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr><!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="acdwrb"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#acdwrb">acdwrb: Grade of a sub-soil being acid</a></th>
	</tr>
	<tr>
		<td>Grade of a sub-soil being acid, e.g. having a pH < 5 and low BS.</td>
	</tr>
	<tr>
		<td>Unit: pH.</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="acdwrb_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> acdwrb_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_acdwrb"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bdricm"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bdricm">bdricm: Depth to bedrock</a></th>
	</tr>
	<tr>
		<td>Depth to bedrock (r horizon) up to 200 cm.</td>
	</tr>
	<tr>
		<td>Unit: cm</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bdricm_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bdricm_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bdricm"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="bdrlog"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#bdrlog">bdrlog: Probability of occurence of r horizon</a></th>
	</tr>
	<tr>
		<td>Probability of occurence of e horizon.</td>
	</tr>
	<tr>
		<td>Unit: Percent</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="bdrlog_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> bdrlog_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_bdrlog"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="histpr"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#histpr">histpr: Cumulative probability of organic soil</a></th>
	</tr>
	<tr>
		<td>Cumulative probability of organic soil based on the TAXOUSDA and TAXNWRB.</td>
	</tr>
	<tr>
		<td>Unit: -.</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="histpr_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> histpr_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_histpr"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="slgwrb"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#slgwrb">slgwrb: Sodic soil grade</a></th>
	</tr>
	<tr>
		<td>Sodic soil grade based on WRB soil types and soil pH.</td>
	</tr>
	<tr>
		<td>Unit: pH</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="slgwrb_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> slgwrb_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_slgwrb"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
</table>


<div id="flo1k" class="anchorcontainer"></div><br>
# <a href="/environment90m/environment90m_layers#flo1k">Stream Flow (FLO1K)</a>
<a href="#top-of-page">Back to top</a> &nbsp; <a href="#meritdem">Next category</a><br>


For stream flow we used the FLO1K dataset which comprises the <b>mean, maximum and minimum annual flow</b> for each year in the period 1960–2015, provided as spatially continuous gridded layers at a high spatial resolution of 30 arc-seconds (ca. 1 km²) (<em>Barbarossa et al. (2018)</em>, see <a href="#references">references</a> below). From this dataset, we only used the data from 1980 - 2010 and averaged it across this time to match the <em>CHELSA observed climate</em> dataset (see <a href="#chelsa">above</a>).


* How to <a href="https://glowabio.github.io/hydrographr/reference/download_env90m_tables.html" target="_blank">download the data</a> using the R package <a href="https://glowabio.github.io/hydrographr/" target="_blank">hydrographr</a>:

<span class="codeblock">
download_flo1k_tables( <br>
subset = c("flo1k"),
tile_ids = c("h00v04"),
download_dir = ".",
download = TRUE)
</span>

* Directory containing all the variables: <a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fflo1k_v1_0" target="_blank">public.igb-berlin.de</a><!--a href="https://public.igb-berlin.de/index.php/apps/files?dir=/environment90m_v.1.0/flo1k_v1_0&fileid=1310533" target="_blank">public.igb-berlin.de</a-->

<table style="width:100%; background-image:none">
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="streamflow"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#streamflow">flo1k: Stream flow</a></th>
	</tr>
	<tr>
		<td>The long-term mean annual flow represents the average of the year-specific FLO1K maps for mean Annual Flow over the period 1980 - 2010.</td>
	</tr>
	<tr>
		<td>Unit: m³/s.<br>Scale: -<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/flo1k_v1_0/h18v02_flow1km_subset_map.png" alt="flo1k_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> flo1k_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_flo1k"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
</table>

<!-- ---------------------------------NEXT------------------------------- -->
<div id="meritdem" class="anchorcontainer"></div><br>
# <a href="/environment90m/environment90m_layers#meritdem">Elevation (MERIT-DEM)</a>
<a href="#top-of-page">Back to top</a> &nbsp; <a href="#cgiar">Next category</a><br>

To represent the elevation variable we used the 90 m resolution Multi-Error-Removed Improved-Terrain Digital Elevation Model (MERIT DEM) v1.0.3 (Yamazaki et al. (2017), see <a href="#references">references</a> below). The error removal procedures have improved the vertical accuracy of this product.

Spatial Resolution: 90m²

* How to <a href="https://glowabio.github.io/hydrographr/reference/download_env90m_tables.html" target="_blank">download the data</a> using the R package <a href="https://glowabio.github.io/hydrographr/" target="_blank">hydrographr</a>:

<span class="codeblock">
download_merit_dem_tables( <br>
subset = c("elev"),
tile_ids = c("h00v04"),
download_dir = ".",
download = TRUE)
</span>

* Directory containing all the variables: <a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fmerit_dem_v1_0_3" target="_blank">public.igb-berlin.de</a><!--a href="https://public.igb-berlin.de/index.php/apps/files?dir=/environment90m_v.1.0/merit_dem_v1_0_3&fileid=1434431" target="_blank">public.igb-berlin.de</a-->

<table style="width:100%; background-image:none">
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="merit"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#merit">elev: Mean elevation</a></th>
	</tr>
	<tr>
		<td>The MERIT DEM represents elevation in meters (mean elevation of the sub-catchment).</td>
	</tr>
	<tr>
		<td>Unit: m</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/merit_dem_v1_0_3/h18v02_elev_subset_map.png" alt="merit_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank"> merit_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_merit"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
</table>


<!-- ---------------------------------NEXT------------------------------- -->
<div id="cgiar" class="anchorcontainer"></div><br>
# <a href="/environment90m/environment90m_layers#cgiar">Aridity and Evapotranspiration (cgiar csi v.3)</a>
<a href="#top-of-page">Back to top</a> &nbsp; <a href="#hy90m">Next category</a><br>


This dataset provides global raster data on <b>evapotranspiration processes and rainfall deficit</b> for potential vegetation growth, at a high spatial resolution of 30 arc-seconds (ca. 1 km²). Global Aridity and Potential Evapotranspiration are both modeled using data available from <em>WorldClim Global Climate Data</em>. The data is available for the 1970 - 2000 period (Zomer and Trabucco (2022), see <a href="#references">references</a> below).

* How to <a href="https://glowabio.github.io/hydrographr/reference/download_env90m_tables.html" target="_blank">download the data</a> using the R package <a href="https://glowabio.github.io/hydrographr/" target="_blank">hydrographr</a>:

<span class="codeblock">
download_cgiar_tables( <br>
subset = c("garid"),
tile_ids = c("h00v04"),
download_dir = ".",
download = TRUE)
</span>

* Directory containing all the variables: <a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fcgiar_csi_v3" target="_blank">public.igb-berlin.de</a><!--a href="https://public.igb-berlin.de/index.php/apps/files?dir=/environment90m_v.1.0/cgiar_csi_v3&fileid=1310797" target="_blank">public.igb-berlin.de</a-->


<table style="width:100%; background-image:none">
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="gevapt"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#gevapt">gevapt: Evapotranspiration</a></th>
	</tr>
	<tr>
		<td>Potential Evapo-Transpiration (ET0) based upon implementation of the FAO-56 Penman-Monteith Reference Evapotranspiration (ET0) equation.</td>
	</tr>
	<tr>
		<td>Unit: mm<br>Scale: -<br>Offset: -</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/cgiar_csi_v3/gevapt_h18v02_subset_map.png" alt="gevapt_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank">gevapt_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_gevapt"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
	<!-- ------------------------ NEXT VAR: ------------------------ -->
	<tr>
		<td><div class="anchorcontainer"></div><div id="garid"></div></td>
	</tr>
	<tr>
		<th class="th1"><a href="/environment90m/environment90m_layers#garid">garid: Aridity Index</a></th>
	</tr>
	<tr>
		<td>Ratio between precipitation and ET0. Values reported have been multiplied by a factor of 10.000</td>
	</tr>
	<tr>
		<td>Unit: -<br>Scale: -<br>Offset: (Values reported have been multiplied by a factor of 10.000)</td>
	</tr>
	<!-- tr>
		<td rowspan="1">
			<img src="/images/environment90m/layer_images/fake_placeholder.png" alt="garid_*.txt" width="320" />
		</td>
		<td><br><br><br><br>
			<ul>
				<li><a href="https://public.igb-berlin.de/index.php/s/wEjgxFK9B32xaMy" target="_blank">garid_*.txt (table)</a></li>
				<li><a href="https://geo.igb-berlin.de/maps/new?layer=geonode:hydrography90m_v1_accumulation_cog&view=True" target="_blank" >[No  visualization on GeoNode]</a></li>
			</ul>
		</td>
	</tr -->
	<tr>
		<td><div id="dynamic_garid"><span style="color:lightgrey">Download link for selected tile</span></div></td>
	</tr>
</table>


<!-- ---------------------------------NEXT------------------------------- -->
<div id="hy90m" class="anchorcontainer"></div><br>
# <a href="/environment90m/environment90m_layers#hy90m">Hydrography90m</a>
<a href="#top-of-page">Back to top</a><br>

The Hydrography90m is a high-resolution (∼90 m) dataset delineating a global stream channel network (<em>Amatulli et al. (2022)</em>, see <a href="#references">references</a> below) and serves as the base of Environment90m. The calculation of Hydrography90m used the MERIT Hydro Digital Elevation Model at 3 arcsec (∼90 m at the Equator) (<em>Yamazaki et al. (2017)</em>, see <a href="#references">references</a> below). The main feature of Hydrography90m is the delineation of small headwater streams. In addition, this dataset includes a number of stream topographic and topological properties. The summary statistics of the Environment90m dataset presented here are calculated for each of the 726 million unique sub-catchments of the Hydrography90m, which also serve as the spatial units in Environment90m.

* How to <a href="https://glowabio.github.io/hydrographr/reference/download_env90m_tables.html" target="_blank">download the data</a> using the R package <a href="https://glowabio.github.io/hydrographr/" target="_blank">hydrographr</a>:

<span class="codeblock">
download_hydrography90m_tables(<br>
subset = c("cti"),
tile_ids = c("h00v04"),
download_dir = ".",
download = TRUE)
</span>

* How to <a href="https://glowabio.github.io/hydrographr/reference/download_tiles.html" target="_blank">download the same variables as spatial data</a> (GeoTIFF and/or geopackage files), using the function <span class="code">download_tiles</span>:

<span class="codeblock">
download_tiles(<br>
variable = "cti",
file_format = "tif",
tile_id = c("h00v04"),
download_dir = ".")
</span>

* Directory containing all the variables: <a href="https://public.igb-berlin.de/index.php/s/zw56kEd25NsQqcQ?path=%2Fhydrography90m_v1_0" target="_blank">public.igb-berlin.de</a><!--a href="https://public.igb-berlin.de/index.php/apps/files?dir=/environment90m_v.1.0/hydrography90m_v1_0&fileid=1428311" target="_blank">public.igb-berlin.de</a-->


For detailed explanations of the variables, please refer to the neighbour page <a href="/hydrography90m/hydrography90m_layers.html">hydrography90m_layers</a>:

<span class="th1"><a href="../hydrography90m/hydrography90m_layers#base-layers">1 base layer:</a></span>

* <a href="../hydrography90m/hydrography90m_layers#flow-accumulation">accumulation</a> <span id="dynamic_accumulation" style="color:lightgrey">(download link for selected tile)</span>


<span class="th1"><a href="../hydrography90m/hydrography90m_layers#stream-slope-layers">4 stream slope layers:</a></span>

* <a href="../hydrography90m/hydrography90m_layers#slope_curv_max_dw_cel">slope_curv_max_dw_cel</a> <span id="dynamic_slope_curv_max_dw_cel" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#slope_curv_min_dw_cel">slope_curv_min_dw_cel</a> <span id="dynamic_slope_curv_min_dw_cel" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#slope_elv_dw_cel">slope_elv_dw_cel</a> <span id="dynamic_slope_elv_dw_cel" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#slope_grad_dw_cel">slope_grad_dw_cel</a> <span id="dynamic_slope_grad_dw_cel" style="color:lightgrey">(download link for selected tile)</span>


<span class="th1"><a href="../hydrography90m/hydrography90m_layers#stream-distance-layers">6 stream distance layers:</a></span>

* <a href="../hydrography90m/hydrography90m_layers#stream_dist_dw_near">stream_dist_dw_near</a> <span id="dynamic_stream_dist_dw_near" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#stream_dist_proximity">stream_dist_proximity</a> <span id="dynamic_stream_dist_proximity" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#stream_dist_up_farth">stream_dist_up_farth</a> <span id="dynamic_stream_dist_up_farth" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#stream_dist_up_near">stream_dist_up_near</a> <span id="dynamic_stream_dist_up_near" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#outlet_dist_dw_basin">outlet_dist_dw_basin</a> <span id="dynamic_outlet_dist_dw_basin" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#outlet_dist_dw_scatch">outlet_dist_dw_scatch</a> <span id="dynamic_outlet_dist_dw_scatch" style="color:lightgrey">(download link for selected tile)</span>


<span class="th1"><a href="../hydrography90m/hydrography90m_layers#stream-distance-layers">5 elevation layers:</a></span>

* <a href="../hydrography90m/hydrography90m_layers#stream_diff_dw_near">stream_diff_dw_near</a> <span id="dynamic_stream_diff_dw_near" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#stream_diff_up_farth">stream_diff_up_farth</a> <span id="dynamic_stream_diff_up_farth" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#stream_diff_up_near">stream_diff_up_near</a> <span id="dynamic_stream_diff_up_near" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#outlet_diff_dw_basin">outlet_diff_dw_basin</a> <span id="dynamic_outlet_diff_dw_basin" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#outlet_diff_dw_scatch">outlet_diff_dw_scatch</a> <span id="dynamic_outlet_diff_dw_scatch" style="color:lightgrey">(download link for selected tile)</span>


<span class="th1"><a href="../hydrography90m/hydrography90m_layers#stream-segment-properties-layers">11 segment properties layers:</a></span>

* <a href="../hydrography90m/hydrography90m_layers#channel_curv_cel">channel_curv_cel</a> <span id="dynamic_channel_curv_cel" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_dist_dw_seg">channel_dist_dw_seg</a> <span id="dynamic_channel_dist_dw_seg" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_dist_up_cel">channel_dist_up_cel</a> <span id="dynamic_channel_dist_up_cel" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_dist_up_seg">channel_dist_up_seg</a> <span id="dynamic_channel_dist_up_seg" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_elv_dw_cel">channel_elv_dw_cel</a> <span id="dynamic_channel_elv_dw_cel" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_elv_dw_seg">channel_elv_dw_seg</a> <span id="dynamic_channel_elv_dw_seg" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_elv_up_cel">channel_elv_up_cel</a> <span id="dynamic_channel_elv_up_cel" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_elv_up_seg">channel_elv_up_seg</a> <span id="dynamic_channel_elv_up_seg" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_grad_dw_seg">channel_grad_dw_seg</a> <span id="dynamic_channel_grad_dw_seg" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_grad_up_cel">channel_grad_up_cel</a> <span id="dynamic_channel_grad_up_cel" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#channel_grad_up_seg">channel_grad_up_seg</a> <span id="dynamic_channel_grad_up_seg" style="color:lightgrey">(download link for selected tile)</span>

<span class="th1"><a href="../hydrography90m/hydrography90m_layers#stream-order-layers">5 stream order layers:</a></span>

* <a href="../hydrography90m/hydrography90m_layers#order_hack">order_hack</a> <span id="dynamic_order_hack" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#order_horton">order_horton</a> <span id="dynamic_order_horton" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#order_shreve">order_shreve</a> <span id="dynamic_order_shreve" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#order_strahler">order_strahler</a> <span id="dynamic_order_strahler" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#order_topo">order_topo</a> <span id="dynamic_order_topo" style="color:lightgrey">(download link for selected tile)</span>


<span class="th1"><a href="../hydrography90m/hydrography90m_layers#flow-index-layers">3 flow index layers:</a></span>

* <a href="../hydrography90m/hydrography90m_layers#cti">cti</a> <span id="dynamic_cti" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#spi">spi</a> <span id="dynamic_spi" style="color:lightgrey">(download link for selected tile)</span>
* <a href="../hydrography90m/hydrography90m_layers#sti">sti</a> <span id="dynamic_sti" style="color:lightgrey">(download link for selected tile)</span>

Some variables are not included in Hydrography90m, so we explain them here:

<span class="th1">10 stream reach layers:</span>

* <b>length:</b> Length of the stream reach <span id="dynamic_length" style="color:lightgrey">(download link for selected tile)</span>
* <b>stright:</b> Straight length / Length of the stream as straight line <span id="dynamic_stright" style="color:lightgrey">(download link for selected tile)</span>
* <b>sinosoid:</b> Sinusoid of the stream reach / Fractal dimension: Stream length/straight stream length <span id="dynamic_sinusoid" style="color:lightgrey">(download link for selected tile)</span>
* <b>cum_length:</b> Accumulated length / Length of stream from source <span id="dynamic_cum_length" style="color:lightgrey">(download link for selected tile)</span>
* <b>out_dist:</b> Distance to outlet / Distance of current stream init from outlet <span id="dynamic_out_dist" style="color:lightgrey">(download link for selected tile)</span>
* <b>source_elev:</b> Source elevation / Elevation of stream init <span id="dynamic_source_elev" style="color:lightgrey">(download link for selected tile)</span>
* <b>outlet_elev:</b> Outlet elevation / Elevation of stream outlet <span id="dynamic_outlet_elev" style="color:lightgrey">(download link for selected tile)</span>
* <b>elev_drop:</b> Elevation drop / Difference between source_elev and outlet_elev + drop outlet <span id="dynamic_elev_drop" style="color:lightgrey">(download link for selected tile)</span>
* <b>out_drop:</b> Outlet drop / Drop at the outlet of the stream <span id="dynamic_out_drop" style="color:lightgrey">(download link for selected tile)</span>
* <b>gradient:</b> Gradient / Mean gradient of the sub-catchment (downstream elevation difference divided by distance) <span id="dynamic_gradient" style="color:lightgrey">(download link for selected tile)</span>

<!-- We decided to ignore these: -->
<!--span class="th1">3 more stream order layers:</span-->

<!--
* <b>order_scheidegger:</b> TODO add description <span id="dynamic_order_scheidegger" style="color:lightgrey">(download link for selected tile)</span>
* <b>order_drwal:</b> TODO add description <span id="dynamic_order_drwal" style="color:lightgrey">(download link for selected tile)</span>
* <b>order_order_topo_dim:</b> TODO add description <span id="dynamic_order_topo_dim" style="color:lightgrey">(download link for selected tile)</span>
-->

<span class="th1">1 stream connectivity layer:</span>

* <b>connections:</b> TODO add description <span id="dynamic_connections" style="color:lightgrey">(download link for selected tile)</span>



<a href="#top-of-page">Back to top</a><br>
# <a href="/environment90m/environment90m_layers#references">References</a>

<b>Environment90m:</b>

* García Márquez, J. R., Grigoropoulou, A., Tomiczek, T., Schürz, M., Bremerich, V., Torres-Cambas, Y., Buurman, M., Amatulli, G., and Domisch, S.: <b>Environment90m</b> - globally standardized environmental variables for freshwater science at high spatial resolution. Earth System Science Data, 18, 1541-1559, <a href="https://doi.org/10.5194/essd-18-1541-2026" target="_blank">doi:10.5194/essd-18-1541-2026</a>, 2026.


<b>Hydrography90m:</b>

* Amatulli, G., Garcia Marquez, J.R., Sethi, T., Kiesel, J., Grigoropoulou, A., Üblacker, M., Shen, L., Domisch, S.: <b>Hydrography90m:</b> A new high-resolution global hydrographic dataset. Earth System Science Data, 14, 4525–4550, <a href="https://doi.org/10.5194/essd-14-4525-2022" target="_blank">doi:10.5194/essd-14-4525-2022</a>, 2022.

<b>Bioclimatic variables:</b>

* Karger, D. N., Conrad, O., Böhner, J., Kawohl, T., Kreft, H., Soria-Auza, R. W., Zimmermann, N. E., Linder, H. P., and Kessler, M.: Climatologies at high resolution for the earth’s land surface areas, Scientific data, 4, 1–20, 2017.
* Karger, D. N., Conrad, O., Böhner, J., Kawohl, T., Kreft, H., Soria-Auza, R. W., Zimmermann, N. E., Linder, H. P., and Kessler, M.: Climatologies at high resolution for the earth’s land surface areas, Scientific Data, 4, 170 122, <a href="https://doi.org/10.1038/sdata.2017.122" target="_blank">doi:10.1038/sdata.2017.122</a>, 2017.
* Karger, D. N., Conrad, O., Böhner, J., Kawohl, T., Kreft, H., Soria-Auza, R. W., Zimmermann, N. E., Linder, H. P., and Kessler, M.: Climatologies at high resolution for the earth’s land surface areas, <a href="https://doi.org/10.16904/envidat.228" target="_blank">doi:10.16904/envidat.228</a>, 2021.
* Ebi, K. L., Hallegatte, S., Kram, T., Arnell, N. W., Carter, T. R., Edmonds, J., Kriegler, E., Mathur, R., O’Neill, B. C., Riahi, K., et al.: A new
scenario framework for climate change research: background, process, and future directions, Climatic Change, 122, 363–372, 2014.
* O’Neill, B. C., Kriegler, E., Ebi, K. L., Kemp-Benedict, E., Riahi, K., Rothman, D. S., Van Ruijven, B. J., Van Vuuren, D. P., Birkmann, J., Kok, K., et al.: The roads ahead: Narratives for shared socioeconomic pathways describing world futures in the 21st century, Global environmental change, 42, 169–180, 2017.

<b>Soil:</b>

* Hengl, T., Mendes de Jesus, J., Heuvelink, G. B. M., Ruiperez Gonzalez, M., Kilibarda, M., Blagotić, A., Shangguan, W., Wright, M. N., Geng, X., Bauer-Marschallinger, B., Guevara, M. A., Vargas, R., MacMillan, R. A., Batjes, N. H., Leenaars, J. G. B., Ribeiro, E., Wheeler, I., Mantel, S., and Kempen, B.: <b>SoilGrids250m:</b> Global gridded soil information based on machine learning, PLOS ONE, 12, e0169 748, <a href="https://doi.org/10.1371/journal.pone.0169748" target="_blank">doi:10.1371/journal.pone.0169748</a>, 2017.

<b>Land Cover:</b>

* ESA: Land Cover CCI Product User Guide Version 2. Tech. Rep. Available at: <a href="https://maps.elie.ucl.ac.be/CCI/viewer/download/ESACCI-LC-Ph2-PUGv2_2.0.pdf" target="_blank">maps.elie.ucl.ac.be/CCI/viewer/download/ESACCI-LC-Ph2-PUGv2_2.0.pdf</a>, Tech. rep., European Space Agency, 2017.
* CCI, E. L. C.: Product user guide version 2.0, UCL-Geomatics: London, UK, 685, 2017.

<b>Aridity and Evapotranspiration:</b>

* Zomer, R. J. and Trabucco, A.: Version 3 of the "Global Aridity Index and Potential Evapotranspiration (ET0) Database": Estimation of Penman-Monteith Reference Evapotranspiration. Available online from the CGIAR-CSI GeoPortal at: <a href="https://cgiarcsi.community/2019/01/24/global-aridity-index-and-potential-evapotranspiration-climate-database-v3/">https://cgiarcsi.community/2019/0124/global-aridity-index-and-potential-evapotranspiration-climate-database-v3/</a>, Tech. rep., CGIAR-320
CSI, <a href="https://cgiarcsi.community/2019/01/24/global-aridity-index-and-potential-evapotranspiration-climate-database-v3">https://cgiarcsi.community/2019/01/24/global-aridity-index-and-potential-evapotranspiration-climate-database-v3</a>, 2022.

<b>Stream flow:</b>

* Barbarossa, V., Huijbregts, M. A. J., Beusen, A. H. W., Beck, H. E., King, H., and Schipper, A. M.: <b>FLO1K,</b> global maps of mean, maximum and minimum annual streamflow at 1 km resolution from 1960 through 2015, Scientific Data, 5, 180 052, <a href="https://doi.org/10.1038/sdata.2018.52" target="_blank">doi:10.1038/sdata.2018.52</a>, 2018.

<b>Elevation</b>

* Yamazaki, D., Ikeshima, D., Tawatari, R., Yamaguchi, T., O’Loughlin, F., Neal, J. C., Sampson, C. C., Kanae, S., and Bates, P. D.: A high-accuracy map of global terrain elevations: Accurate Global Terrain Elevation map, Geophysical Research Letters, 44, 5844–5853, <a href="https://doi.org/10.1002/2017GL072874" target="_blank">doi:10.1002/2017GL072874</a>, 2017.

<br>
<br>

<a href="#top-of-page">Back to top</a>
