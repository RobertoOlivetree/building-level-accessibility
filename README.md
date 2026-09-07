# Building-Level Accessibility and Spatial Aggregation

## Overview

This repository contains the reproducible analytical workflow for a building-level pedestrian accessibility and spatial aggregation study conducted in Porto, Portugal.

The workflow uses the building level as the reference spatial representation and evaluates how aggregation changes accessibility variability, spatial dependence and the retention of local intervention priorities. Adults aged 65 years and over provide the demographic and mobility context. Population is introduced only after construction of the Urban Attractiveness Index (UAI), through the Ageing Accessibility Vulnerability Index (AAVI), which is used as a complementary territorial screening measure.

The analysis includes:

- allocation of the population aged 65 years and over from 2021 BGRI statistical subsections to residential buildings;
- building-level pedestrian accessibility for the seven Porto parishes;
- a fixed 800 m pedestrian-network catchment;
- raster-directional slope derived from a 2 m Digital Terrain Model;
- flat and normalised Tobler-adjusted walking times at 0.5, 0.7 and 0.9 m/s;
- 10, 15 and 20 minute walking-sensitivity analysis;
- Principal Component Analysis (PCA) and construction of the UAI;
- equal-weight, imputation and complete-case robustness checks;
- Global Moran's I and Local Indicators of Spatial Association (LISA);
- spatial aggregation using 100 m, 250 m and 500 m regular grids and 2021 BGRI statistical subsections;
- variance-loss, spatial-dependence and priority-retention diagnostics;
- sensitivity of priority identification at 5%, 10% and 20% lower-UAI thresholds;
- AAVI as a post-UAI territorial demographic screening measure.

## Repository structure

```text
notebooks/
    01_allocate_population_65plus.ipynb
    02a_pedestrian_accessibility_aldoar_foz_nevogilde.ipynb
    02b_pedestrian_accessibility_bonfim.ipynb
    02c_pedestrian_accessibility_campanha.ipynb
    02d_pedestrian_accessibility_cedofeita.ipynb
    02e_pedestrian_accessibility_lordelo_ouro_massarelos.ipynb
    02f_pedestrian_accessibility_paranhos.ipynb
    02g_pedestrian_accessibility_ramalde.ipynb
    03_integrate_porto_and_walking_sensitivity.ipynb
    04_uai_aavi_spatial_aggregation.ipynb
    README_EXECUTION_ORDER.md

data/
    raw/
    intermediate/
    processed/

results/
    tables/
    figures/
    spatial/

docs/
    DATA_DICTIONARY.md
    EXPECTED_RESULTS.md

README.md
requirements.txt
environment.yml
CITATION.cff
LICENSE
.gitignore
