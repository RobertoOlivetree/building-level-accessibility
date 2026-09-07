# Raw data

This directory documents the raw spatial data required to reproduce the analysis.

Large source datasets and third-party data are not necessarily stored directly in this repository. Where redistribution is not appropriate or practical, the original source and acquisition instructions are provided below.

## Required datasets

### 1. Residential building footprints

**Source:** OpenStreetMap / Geofabrik  
**Purpose:** Building-level origins for the accessibility analysis.

The original OpenStreetMap building layer was extracted for the municipality of Porto. Non-residential buildings, invalid geometries and records unsuitable for the final analytical universe were removed during preprocessing.

Expected working file:

`edificios.csv`

The final analytical universe contains 31,664 residential buildings.

---

### 2. Pedestrian network

**Source:** OpenStreetMap / Geofabrik  
**Purpose:** Network-based pedestrian accessibility modelling.

The pedestrian network is represented as a directed graph. Residential buildings and service destinations are connected to the pedestrian network before shortest-path calculation.

The network is used to calculate:

- pedestrian-network distance;
- flat-terrain travel time;
- slope-adjusted travel time;
- origin-destination accessibility within an 800 m network catchment.

OpenStreetMap data are subject to the Open Database License (ODbL).

---

### 3. BGRI 2021 statistical subsections

**Source:** Instituto Nacional de Estatística (INE), 2021 Population Census  
**Purpose:** Spatial allocation of the population aged 65 years and over and census-based aggregation analysis.

Expected working file:

`BGRI2021_1312.gpkg`

Population counts for residents aged 65 years and over are redistributed from BGRI statistical subsections to residential buildings in proportion to building footprint area.

The official subsection totals are preserved through a reconciliation procedure after integer rounding.

---

### 4. Digital Terrain Model

**Source:** Direção-Geral do Território (DGT)  
**Spatial resolution:** 2 m  
**Purpose:** Calculation of directional pedestrian-network slope.

The Digital Terrain Model is used at its native resolution to derive raster-directional gradients along pedestrian-network edges.

These gradients are used to calculate slope-adjusted walking costs through the normalised Tobler hiking function.

Because of file size, the complete DTM is not stored in this GitHub repository.

---

### 5. Services and urban amenities

The final service inventory contains 393 destinations distributed across seven categories:

- 100 banks;
- 111 supermarkets;
- 105 pharmacies;
- 33 parks and gardens;
- 24 post offices;
- 18 health centres;
- 2 hospitals.

Sources include:

- Porto Digital Open Data Portal;
- Google Maps;
- Google Street View;
- INFARMED;
- SNS;
- institutional and corporate sources.

The service inventory was compiled and manually verified in May 2026.

Third-party source material from Google Maps and Google Street View is not redistributed as raw data in this repository.

## Coordinate reference systems

Raw datasets may use different coordinate reference systems.

The analytical workflow harmonises spatial data using:

- EPSG:4326 for geographic coordinates where required;
- EPSG:3763 for projected spatial analysis in mainland Portugal.

## Reproducibility

The notebooks in the `notebooks/` directory document the complete processing sequence from raw data to the final analytical outputs.

The expected execution order is:

1. `01_allocate_population_65plus.ipynb`
2. `02a–02g_pedestrian_accessibility_*.ipynb`
3. `03_integrate_porto_and_walking_sensitivity.ipynb`
4. `04_uai_aavi_spatial_aggregation.ipynb`

Intermediate and processed datasets should be stored in the corresponding `data/intermediate/` and `data/processed/` directories.

## Data availability

A reproducible archive associated with the research will be deposited in Zenodo. Where licensing or file-size constraints prevent redistribution of raw source datasets, the repository will provide source information and instructions for obtaining the original data.
