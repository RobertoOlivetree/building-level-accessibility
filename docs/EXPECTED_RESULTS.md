# Expected results and validation targets

This file records the principal manuscript-level values that should be reproduced by the workflow when the documented working inputs are used.

Small floating-point differences may occur across library/platform versions, but counts and substantive results should remain consistent. Several key counts are enforced directly by notebook assertions when `STRICT_MANUSCRIPT_VALIDATION = True`.

## Analytical universe

- Residential buildings in final municipal accessibility universe: **31,664**
- Buildings with no accessible destination within the 800 m network catchment: **420** (**1.33%**)
- Mean accessible destinations per building: **16.18**
- Mean accessible service categories per building: **4.40**
- Mean network distance to accessible destinations: **540.13 m**
- Mean Tobler-adjusted travel time at 0.7 m/s: **13.56 min**

## Population aged 65+

- Municipal BGRI total: **60,216**
- Population allocated to eligible residential buildings: **58,748**
- Population retained in the final network-validated building universe: **58,203**
- Retained share of municipal population aged 65+: **96.7%**

## PCA diagnostics

- KMO: **0.773**
- Bartlett's test: **χ² = 115,319.19**, **df = 28**, **p < .001**
- PC1 explained variance: **49.75%**
- PC2 explained variance: **17.87%**
- Cumulative PC1 + PC2: **67.62%**

### PC1-derived UAI weights

| Variable | Weight |
|---|---:|
| Banks | 0.209 |
| Supermarkets | 0.208 |
| Pharmacies | 0.204 |
| Post offices | 0.143 |
| Health centres | 0.090 |
| Parks and gardens | 0.083 |
| Hospitals | 0.040 |
| Proximity | 0.023 |

## UAI robustness

PCA-weighted versus equal-weight UAI:

- Pearson correlation: **0.973**
- Spearman correlation: **0.987**
- Lower-decile priority retention: **84.79%**
- Priority Jaccard similarity: **0.736**

## Building-level spatial autocorrelation

Primary KNN specification: **k = 20**

- Moran's I: **0.979**
- Permutation p-value: **0.001**

KNN sensitivity:

| k | Moran's I |
|---:|---:|
| 8 | 0.987 |
| 12 | 0.984 |
| 16 | 0.981 |
| 20 | 0.979 |
| 24 | 0.977 |
| 32 | 0.973 |

## Spatial aggregation: variance and Moran's I

| Spatial representation | Variance of unit means | Reduction vs building | Reconstructed building variance | Reduction vs building | Moran's I |
|---|---:|---:|---:|---:|---:|
| Building | 0.0435 | 0.00% | 0.0435 | 0.00% | 0.979 |
| 100 m grid | 0.0331 | 23.76% | 0.0424 | 2.46% | 0.917 |
| BGRI statistical subsections | 0.0307 | 29.42% | 0.0387 | 10.95% | 0.684 |
| 250 m grid | 0.0296 | 31.88% | 0.0408 | 6.14% | 0.776 |
| 500 m grid | 0.0264 | 39.28% | 0.0381 | 12.43% | 0.569 |

## Spatial aggregation: agreement and priority retention

Primary lower-decile priority definition uses a tie-aware threshold.

| Spatial representation | Pearson | Spearman | Priority retention | Missed priority | Jaccard |
|---|---:|---:|---:|---:|---:|
| 100 m grid | 0.988 | 0.988 | 88.61% | 11.39% | 0.795 |
| BGRI statistical subsections | 0.944 | 0.940 | 57.97% | 42.03% | 0.406 |
| 250 m grid | 0.969 | 0.968 | 77.75% | 22.25% | 0.625 |
| 500 m grid | 0.936 | 0.940 | 64.53% | 35.47% | 0.476 |

## Walking-sensitivity reference

At **0.7 m/s** and a **15 minute** travel-time threshold:

| Model | Mean accessible destinations | Mean accessible categories | Buildings with no accessible destination |
|---|---:|---:|---:|
| Flat | 9.97 | 3.60 | 4.04% |
| Tobler-adjusted | 9.27 | 3.44 | 5.37% |

## Interpretation safeguards

- The building level is the reference representation for aggregation comparisons.
- The UAI is an analytical instrument rather than the principal methodological novelty.
- Population aged 65+ is introduced after UAI construction and is not included in the PCA.
- AAVI is a complementary territorial screening measure of the spatial coincidence between older population and lower UAI; it is not a validated individual vulnerability index.
