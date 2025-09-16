# LiveEO

LiveEO AI Team Data Engineer Internship 2025
Author: Emma L Underwood
Date created: 15.09.2025
Last update: 16.09.2025

## Backstory

Data pre-processing to generate image pairs for training a change-detection model.
Reproducible workflow that explores metadata of image footprints between SAR and optical data.
Important: Each chosen pair will become a training sample, good training data = better change detectionability.

## Data provided

* **capella\_archive.parquet** – records of SAR satellite images from the Capella satellite, with metadata and geometries (geom) of their image footprints.
* **capella\_stac.parquet** – even more metadata information of these satellite imagery.
* **skysat.parquet** – exotic records of OPTICAL satellite data from the SkySat satellite constellation, aligned in space and time with the Capella images.

## Tasks

### Objective 1: Explore data

* Describe differences between SAR and Optical, give key differences and specific use cases
* Explore the data (Capella)
* Map their info and how the capsules relate
* Use python

### Objective 2: Assemble Capella pairs

* Find matching image pairs in the SAR(Capella) data - use **capella\_archive.parquet**
* Find before and after images of same location, that are temporally close:

  * geometries/footprints must intersect by > 95%
  * 7-14 days apart
  * similar acquisition properties (use extra info in capella\_stac.parquet) - e.g., orbital properties, polarization, acquisition mode, angles - but also other metadata that might make them incompatible for change detection

### Bonus objective: Find Quartets (SAR-optical double pairs) that match in time and space

* For each Capella SAR chosen pair, check the optical imagery (Skysat) for any appropriate images that:

  * withing 2 days of each SAR
  * Overlap spatially > 95% (geom footprint)
  * Note how many quartets are available in the dual data

## Deliverables

### Objective 1: Explore data

* \[ ] Diff between SAR and optical, and use cases: see presentation slide venn diagram
* \[ ] Summary report - summarise Capella files and metadata showing stats, maps: Section name "data_exploration_report"

### Objective 2: Assemble Capella pairs

* \[ ] Table in report - summary (count) of all filtered pairs found
* \[ ] Map - display matching pairs (see strict_pairs_map_ELU_16092025.html)
* \[ ] write out metadata steps and filtering methods: see presentation slides

### Repository structure

📁 PROJECT\_ROOT/

│

├── 📁 data/

│   ├── 📁 raw/                    \[INPUT DATA - Not in Git]

│   │   ├── 📄 capella\_archive.parquet     (~125k SAR images with geometries)

│   │   ├── 📄 capella\_stac.parquet        (STAC metadata)

│   │   └── 📄 skysat.parquet               (Optical imagery - optional)

│   │

│   └── 📁 output/                  \[PROCESSED RESULTS]

│       │

│       ├── 📊 EXPLORATION OUTPUTS

│       │   ├── 📄 data\_exploration\_detailed.json    (Complete statistics)

│       │   └── 📄 data\_exploration\_report.html      (Formatted report)

│       │

│       ├── 🔄 PAIR MATCHING OUTPUTS

│       │   ├── 📄 pairs\_strict\_1deg.parquet        (Highest quality pairs)

│       │   ├── 📄 pairs\_moderate\_2.0deg.parquet      (Balanced quality/quantity)

│       │   └── 📄 pairs\_relaxed\_5.0deg.parquet      (Maximum quantity)

│       │

│       ├── 🗺️ VISUALISATION OUTPUTS

│       │   └── 📄 strict_pairs_map_ELU_16092025.html                   (Interactive Folium map)

├── 📄 LiveEO_capella_pairs.ipynb     \[MAIN PROCESSING PIPELINE]

├── 📄 .gitignore                  \[Excludes large data files and derived metadata]

└── 📄 README.md                   \[Project documentation][](https://github.com/GeoEmma/LiveEO)

### Summary presentation and visual report

[canva.com/geoemma_pres]([https://www.canva.com/design/DAGzCb8joTM/nPVwQkb3AdVZH0OdEDPAdw/edit](https://www.canva.com/design/DAGzCb8joTM/vli508hT3hssYSsTtEexSg/view?utm_content=DAGzCb8joTM&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=had479e8a41))


