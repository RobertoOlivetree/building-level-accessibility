# Notebook execution order

The notebooks assume the following repository structure:

- `notebooks/`
- `data/raw/`
- `data/intermediate/`
- `data/processed/`
- `results/tables/`
- `results/figures/`
- `results/spatial/`

Required files in `data/raw/`:

- `edificios.csv`
- `servicos.csv`
- `freguesia.csv`
- `rede_final_ligada.csv`
- `MDT_Porto_clip.tif`
- `BGRI2021_1312.gpkg`

Run in this order:

1. `01_allocate_population_65plus.ipynb`
2. `02a` to `02g` parish accessibility notebooks
3. `03_integrate_porto_and_walking_sensitivity.ipynb`
4. `04_uai_aavi_spatial_aggregation.ipynb`

Generated files are written to `data/intermediate/`, `data/processed/`
and `results/`; they are not written into `notebooks/`.

The notebooks deliberately retain the original analytical source/output
field names such as `numero_servicos_proximos`,
`distancia_media_servicos` and the original service-category labels where
those strings are part of the existing data schema. Notebook narrative,
Python identifiers and publication-facing diagnostics are in English.
