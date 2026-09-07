# Building-Level Accessibility and Spatial Aggregation

## Reproducible workflow

This repository contains the reproducible analytical workflow supporting the study:

**From buildings to spatial units: How spatial aggregation reshapes accessibility evidence and intervention priorities**

The workflow evaluates pedestrian accessibility at the building level in Porto, Portugal, with mobility assumptions adapted to adults aged 65 years and over. It also examines how spatial aggregation affects accessibility variability, spatial dependence and the preservation of local intervention priorities.

The analysis includes:

- building-level pedestrian accessibility;
- an 800 m pedestrian-network catchment;
- directed pedestrian networks;
- raster-directional slope derived from a 2 m Digital Terrain Model;
- normalised Tobler-adjusted walking times;
- walking speeds of 0.5, 0.7 and 0.9 m/s;
- sensitivity analysis at 10, 15 and 20 minutes;
- population allocation for residents aged 65 years and over;
- Principal Component Analysis (PCA);
- Urban Attractiveness Index (UAI);
- Ageing Accessibility Vulnerability Index (AAVI);
- Global Moran's I and Local Indicators of Spatial Association (LISA);
- spatial aggregation using 100 m, 250 m and 500 m regular grids and BGRI statistical subsections;
- priority-retention analysis using 5%, 10% and 20% thresholds.

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
.gitignoree MIT License.
MIT License
