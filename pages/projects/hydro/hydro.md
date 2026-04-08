---
layout: page-fullwidth
classes: wide
title: "Monitoring of Freshwater at High Spatio-temporal Resolutions"
meta_title: "Monitoring_of_Freshwater"
permalink: "pages/projects/hydro/hydro"
header:
  image_fullwidth: landing_page5.jpeg
  caption: "Photo by Fjona Shkarpa"
  caption_url: "https://www.spatial-ecology.net/pages/about_us/about_us"
---

The overarching goal of this project is to revolutionise our understanding of the fundamental principles that govern water regimes in streams and lakes worldwide. The project will capture the multi-dimensional aspects of flow regimes (river discharge) and model hydraulics using a wide range of high resolution geo-datasets integrated with gauging station data in a machine learning framework. The preliminary research below lays the foundation for this challenging project.

#### Project presentation

### Global Monitoring of Fresh Water at High Spatial and Temporal Resolutions:

### Assessing Stream and Lake Hydrological/Physical Features within a Machine Learning Framework

JPL-NASA: Earth Science Seminar Thursday, 29 August 2019

Presented by Giuseppe Amatulli, Yale School of Forestry and Environmental Studies, Yale Center for Research Computing, Yale University  


<iframe width="950" height="500" src="https://www.youtube.com/embed/MangFrPYDMM?si=VGjBxTvFP4rOXO0E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; 
clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
\\
\\
Lakes and rivers process a significant quantity of fresh water, which is among the most vulnerable resources in nature. The physico-chemical characteristics of each watershed or stream are the result of complex interactions among several environmental variables. These variables regulate discharge regimes and stream profiles, such as rainfall, evapotranspiration, soil infiltration and retention, geomorphology, land use, and snow cover, among others. Current knowledge of stream flow trends in rural areas and developing countries is limited and fragmented, and small streams are often not represented. A full geo-analysis is needed to capture these stream features. Freshwater quantification at high spatial resolution is therefore essential to this aim, and also the first step towards a comprehensive assessment of the global water cycle. The project captures the multi-dimensional aspects of the flow regimes (monthly discharge) and model hydraulics worldwide, using a broad range of 90m geo-datasets and gauging station data in a machine learning framework. This work will be the most comprehensive hydrological model based on a high dimensional data-driven approach able to assess stream network location, width, depth, and water flow. The overarching goal of this research is to revolutionize our understanding of the fundamental principles that govern freshwater discharge regimes worldwide.

### Status of the project  (update on 1st of July 2020)

Thanks to our 20+ years of experience in processing large geographic data we are advancing at a very fast pace. We are running our computation mainly with three open-source geographic software  GRASS GDAL PKTOOLS (written in C & C++) embedded under Bash environment.  These tools provide fast and scalable computation for raster-based workflows. Besides, the use of Bash as a glueing language allows to the integration of additional tools such as awk & sort & grep & etc. for text manipulation. While the processing language may be considered out of date, it is still one of the fastest ways to process large data and utilise pre-compiled C tools.

At this point, the stream network and the basins have been delineated at high precision and we are in the process of accumulating all the downstream predictor variables. We have started with TERRACLIMATE which includes several fundamental predictors. The entire TERRACLIMATE dataset will be used for testing the Machine Learning algorithms. Based on the initial results, we will refine our methodology by inserting new predictors, identify outliers in the observation archive, adjust and define the observation station sampling, and so on.

We have also started to manipulate the GSIM to extract pixel values from TERRACLIMATE at station locations.

In the summer months of 2020, we will work towards having a first draft of the global monthly discharge for the 1958-2016 time period.

### Methodology

- **Task 1) Dataset archive**
    - **Task 1.a) Observations: gauge station data: discharge + geochemistry (GSIM + geochemistry, [see demo](http://spatial-ecology.net/gsim-temporal-and-spatial-analyis/), ongoing)**
    - **Task 1.b) Predictors: remote sensing and geographic data (completed)**
    - **Task 1.c) Pre-processing predictor datasets (completed)**
- **Task 2) Extraction of hydrographic features from DEM**
    - **Task 2.a) Stream network and basin delineation (completed, [see demo](http://spatial-ecology.net/hydrography-demo/))**
    - **Task 2.b) Compute other stream morphology properties (ongoing)**
- **Task 3) Freshwater-specific environmental predictors**
    - **Task 3.a) Compute stream variables (TERRACLIMATE completed, [see demo](http://spatial-ecology.net/compute-stream-variables/), the rest is ongoing)**
    - **Task 3.b) Observation snapping and stream-predictors extraction at gauge location (ongoing)**
- **Task 4) Geo-data-fusion within a machine learning framework**
    - **Task 4.a) Training and testing splitting procedure (testing phase with TERRACLIMATE)**
    - **Task 4.b) Machine learning algorithm selection (testing phase with Random Forest)**
    - **Task 4.c) Model evaluation and error metrics (acquiring scientific knowledge)**
    - **Task 4.d) Predict response variables and uncertainty in ungauged locations (under development)**
    - **Task 4.e) Variables importance at global and local levels (under development)**
- **Task 5) Web-GIS development (completed prototype, [see demo](https://openlandmap.org/#/?base=Stamen%20\(OpenStreetMap\)&center=-21.4889,-41.3608&zoom=9&opacity=80&layer=hyd_ann.streamflow_flo1k.mean&time=2015))**


#### Global Monitoring of Fresh Water at High Spatial and Temporal Resolutions

- [Monitoraggio globale delle risorse di acqua dolce (in Italian)](http://spatial-ecology.net/wp-content/uploads/2020/02/monitoraggioGlobaleAmatulli.pdf).


#### Water quality (**[see demo)](http://spatial-ecology.net/projects-water-quality-np/)**

- [Estimating nitrogen and phosphorus concentrations in streams and rivers, within a machine learning framework (Scientific Data, 2020)](https://www.nature.com/articles/s41597-020-0478-7)


#### Basin delineation and stream network extraction at global level

- [High-resolution stream network delineation using digital elevation models: assessing spatial accuracy](http://spatial-ecology.net/wp-content/uploads/2018/10/Amatulli_et_al_geomorphometry.pdf)
- [Watershed and stream network delineation using digital elevation models and spectral satellite information](http://spatial-ecology.net/wp-content/uploads/2018/10/GeoComputation_conference.pdf)
- [Hydrographies MERIT-Hydro derived (demo)](http://spatial-ecology.net/hydrography-demo/)


#### Geomorphometric/Topographic/Environmental variables at global level

- [Geomorpho90m, empirical evaluation and accuracy assessment of global high-resolution geomorphometric layers (Scientific Data, 2020)](https://www.nature.com/articles/s41597-020-0479-6)
- [Geomorpho90m: Global high-resolution geomorphometry variables for environmental modelling (poster)](http://spatial-ecology.net/wp-content/uploads/2018/10/Geomorpho90m.pdf)
- [Geomorpho90m: Global high-resolution geomorphometry variables for environmental modelling (geodaset overview)](http://www.spatial-ecology.net/dokuwiki/doku.php?id=topovar90m)
- [Geomorpho90m: Global high-resolution geomorphometry variables for environmental modelling (WGS84 downloading repository)](http://opentopo.sdsc.edu/dataspace/dataset?opentopoID=OTDS.012020.4326.1)
- [Geomorpho90m: Global high-resolution geomorphometry variables for environmental modelling (web-GIS visualization)](https://landgis.opengeohub.org/#/?base=Stamen%20\(OpenStreetMap\)&center=41.8890,-89.7607&zoom=5&opacity=80&layer=dtm_rough-magnitude_merit.dem_m)
- [A suite of global, cross-scale topographic variables for environmental and biodiversity modelling](http://spatial-ecology.net/wp-content/uploads/2018/10/Topography.pdf)
- [Near-global freshwater-specific environmental variables for biodiversity analyses in 1 km resolution](http://spatial-ecology.net/wp-content/uploads/2018/10/stream_variables.pdf)

### High resolution Digital Elevation Models: extracting geomorphometric features  and hydrography.

<iframe width="950" height="500" src="https://www.youtube.com/embed/tYawKKkmvY8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; 
clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> 

#### Project team

The project's research team brings together several years of experience in large geographic data and machine learning model implementation. The team members' outstanding credentials in the environmental and computer sciences, statistical modelling and hydrology offer the requisite skills to achieve project objectives.

**PI:**  Dr. **Giuseppe Amatulli** Research Scientist at Yale University (USA). Expertise: Geocomputation, data analysis, GIS, remote sensing , big geo-dataset processing, hydrology.

**Co-PI:** Dr. **George H. Allen** Assistant Professor at Texas A&M University (USA). Expertise: hydrology, remote sensing, GIS, data analysis, water resources.

**Scientists: 2 Post-Docs** with expertise hydrology, machine learning and geocomputation (to be selected)

**Advisor:** Prof. **Peter Raymond** Professor at Yale University (USA). Expertise: (USA). Expertise: hydro-chemistry, water resources, freshwater ecology.

**Advisor:** Dr. **Longzhu Shen** Research Scientist at University of Cambridge (UK). Expertise: modeller, data analysis, big-data processing, machine learning, chemistry.

**Advisor:** Dr. **Sami Domisch** Research Scientist at Leibniz-Institute of Freshwater Ecology and Inland Fisheries (Germany). Expertise: freshwater biodiversity, biogeography, modelling and data analysis, massive data processing, machine learning

**Collaborator:** Mr. **Richard Barnes** PhD Student at University of Berkeley. Expertise: computer scientist, developer, data analysis

**Collaborator:** Mr. **Paolo Corti** Geospatial Engineering consultant at Spatial Ecology. Expertise: computer scientist, web-GIS developer

**Collaborator:** Mr. **Tushar Sethi** Director, Spatial Ecology (UK). Expertise: Water and waste management technologies; translating scientific research into applied solutions.
