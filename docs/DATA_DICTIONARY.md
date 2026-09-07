# Data dictionary

This document defines the principal fields used across the reproducible workflow. It focuses on fields required to understand or reproduce the reported analysis rather than every temporary diagnostic variable.

## Raw / prepared input fields

### `edificios.csv`

| Field | Meaning |
|---|---|
| `osm_id` | Building identifier retained from the prepared OpenStreetMap-derived building input. |
| `geometry_wkt` or `geometry` | Building geometry encoded as WKT and interpreted as EPSG:4326 by the notebooks. |

### `servicos.csv`

| Field | Meaning |
|---|---|
| `Name` | Destination name or identifier. |
| `Category` | Service category used by the accessibility model. |
| `Longitude` | Destination longitude in geographic coordinates. |
| `Latitude` | Destination latitude in geographic coordinates. |

Analytical service categories: `Bancos`, `Supermercados`, `Farmacias`, `CTT`, `Parques e jardins`, `Centro Saude`, `Hospitais`.

### `freguesia.csv`

| Field | Meaning |
|---|---|
| `Official Name Parish` | Official parish name used for study-area selection. |
| `Geo Shape` | Parish geometry encoded as GeoJSON. |

### `BGRI2021_1312.gpkg`

| Field | Meaning |
|---|---|
| `N_INDIVIDUOS_65_OU_MAIS` | Population aged 65 years and over in each BGRI statistical subsection. |
| `DTMNFRSEC21` | BGRI statistical-subsection identifier used by Notebook 04. |
| `SUBSECCAO` | Alternative subsection identifier accepted by Notebook 01 when available. |

## Population-allocation output

File: `data/intermediate/population/population_65plus_by_building.csv`

| Field | Meaning |
|---|---|
| `osm_id` | Building identifier. |
| BGRI identifier | Statistical subsection assigned to the building. |
| `footprint_area_m2` | Building footprint area in square metres. |
| `pop_64_mais` | Estimated population aged 65 years and over allocated to the building. |

## Parish accessibility output

Files: `resultados_acessibilidade_800m_<parish>_global.csv`

| Field | Meaning |
|---|---|
| `osm_id` | Building identifier. |
| `geometry_wkt` | Building geometry written as WKT. |
| `dist_to_network` | Minimum straight-line distance from the building geometry/centroid to the selected pedestrian network. |
| `ligado_rede` | Boolean flag indicating whether the building satisfies the network-connection criterion. |
| `numero_servicos_proximos` | Number of accessible destinations within the fixed 800 m network catchment. |
| `distancia_media_servicos` | Mean network distance to accessible destinations, in metres. |
| `distancia_minima_servico` | Minimum network distance to an accessible destination, in metres. |
| `servico_min_id` | Identifier/name of the nearest accessible destination by network distance. |
| `servico_min_categoria` | Category of the nearest accessible destination. |
| `Bancos` | Accessible bank count within 800 m network distance. |
| `Supermercados` | Accessible supermarket count within 800 m network distance. |
| `Farmacias` | Accessible pharmacy count within 800 m network distance. |
| `CTT` | Accessible post-office count within 800 m network distance. |
| `Parques e jardins` | Accessible park/garden count within 800 m network distance. |
| `Centro Saude` | Accessible health-centre count within 800 m network distance. |
| `Hospitais` | Accessible hospital count within 800 m network distance. |
| `tempo_medio_seg__flat_0p5` | Mean flat-terrain travel time at 0.5 m/s, seconds. |
| `tempo_medio_seg__flat_0p7` | Mean flat-terrain travel time at 0.7 m/s, seconds. |
| `tempo_medio_seg__flat_0p9` | Mean flat-terrain travel time at 0.9 m/s, seconds. |
| `tempo_medio_seg__tobler_0p5` | Mean Tobler-adjusted travel time at 0.5 m/s, seconds. |
| `tempo_medio_seg__tobler_0p7` | Mean Tobler-adjusted travel time at 0.7 m/s, seconds. |
| `tempo_medio_seg__tobler_0p9` | Mean Tobler-adjusted travel time at 0.9 m/s, seconds. |
| `tempo_min_seg__*` | Minimum travel time under the corresponding flat or Tobler scenario, seconds. |
| `tempo_medio_servicos_seg` | Main downstream mean travel-time field; equal to `tempo_medio_seg__tobler_0p7`. |
| `tempo_minimo_servico_seg` | Main downstream minimum travel-time field; equal to `tempo_min_seg__tobler_0p7`. |
| `cenario_principal` | Main downstream travel-time scenario (`tobler_0p7`). |
| `distancia_max_m` | Fixed network-distance catchment, 800 m. |
| `time_hard_threshold` | Indicates that no hard travel-time threshold is imposed in the primary 800 m accessibility calculation. |

## Origin–destination output

Files: `resultados_od_800m_<parish>_global.csv` and `data/processed/porto_origin_destination_800m.csv`

| Field | Meaning |
|---|---|
| `building_id` | Origin building identifier. |
| `service_id` | Destination identifier/name. |
| `service_category` | Destination category. |
| `network_distance_m` | Shortest pedestrian-network distance from origin to destination, metres. |
| `tobler_unit_cost_m` | Slope-adjusted Tobler unit cost before division by the walking-speed scenario. |
| `origin_node` | Graph node associated with the origin. |
| `service_node` | Graph node associated with the destination. |
| `source_parish` | Parish source added during municipal integration. |

## Municipal accessibility fields added by Notebook 03

| Field | Meaning |
|---|---|
| `ficheiro_origem` | Parish source identifier. |
| `minimo_zero_snap` | Quality-control flag for zero minimum network distance. |
| `tobler_qc_excluded` | Quality-control flag for implausibly large mean Tobler travel time. |

## PCA / UAI fields

| Field | Meaning |
|---|---|
| `proximity` | Reversed, min-max-normalised mean Tobler travel-time indicator at 0.7 m/s; higher values indicate more favourable proximity. |
| `uai` | Urban Attractiveness Index, rescaled to [0,1]. Higher values indicate more favourable accessibility/attractiveness under the model. |
| `pca_proximity` | Building-level proximity variable used in the PCA/UAI workflow. |

PCA variables are: banks, supermarkets, pharmacies, post offices, health centres, parks/gardens, hospitals and proximity. Population is not included in the PCA.

## AAVI

| Field | Meaning |
|---|---|
| `AAVI` | Ageing Accessibility Vulnerability Index, calculated as `pop_64_mais × (1 − uai)`. It is a territorial screening measure and is not an individual-level vulnerability score. |

## Aggregation outputs

Unit-level spatial outputs include the following principal fields:

| Field | Meaning |
|---|---|
| `unit_id` | Identifier of the grid cell or BGRI statistical subsection. |
| `unit_mean` | Mean building-level UAI within the spatial unit. |
| `n_buildings` | Number of buildings assigned to the unit. |
| `unit_range` | Within-unit UAI range. |
| `unit_std` | Within-unit UAI standard deviation. |

Assignment CSVs link each building `osm_id` to its `unit_id` and corresponding `unit_mean`.

## Priority definition

The primary intervention-priority reference is the lower 10% of building-level UAI values using a tie-aware cutoff. Sensitivity is also evaluated at 5% and 20%.
