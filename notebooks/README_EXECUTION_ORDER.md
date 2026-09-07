# Notebook execution order

The notebooks assume the following repository structure:

```text
notebooks/
data/raw/
data/intermediate/
data/processed/
results/tables/
results/figures/
results/spatial/
```

Required working inputs in `data/raw/`:

- `edificios.csv`
- `servicos.csv`
- `freguesia.csv`
- `rede_final_ligada.csv`
- `MDT_Porto_clip.tif`
- `BGRI2021_1312.gpkg`

Run in this order:

1. `01_allocate_population_65plus.ipynb`
2. `02a_pedestrian_accessibility_aldoar_foz_nevogilde.ipynb`
3. `02b_pedestrian_accessibility_bonfim.ipynb`
4. `02c_pedestrian_accessibility_campanha.ipynb`
5. `02d_pedestrian_accessibility_cedofeita.ipynb`
6. `02e_pedestrian_accessibility_lordelo_ouro_massarelos.ipynb`
7. `02f_pedestrian_accessibility_paranhos.ipynb`
8. `02g_pedestrian_accessibility_ramalde.ipynb`
9. `03_integrate_porto_and_walking_sensitivity.ipynb`
10. `04_uai_aavi_spatial_aggregation.ipynb`

The seven parish notebooks are independent and may be executed in any order after the raw inputs are available. Notebook 03 requires all seven parish outputs. Notebook 04 requires both Notebook 01 and Notebook 03 outputs.

Generated files are written to `data/intermediate/`, `data/processed/` and `results/`; they are not written into `notebooks/`.

The workflow retains Portuguese analytical field names where they are part of the validated data schema. Narrative text, methodological documentation and validation messages are in English.
