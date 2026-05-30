# place-matters-indonesia

District-year panel analysis of state repression and protest mobilization in Indonesia (2019–2024). Tests whether built-up density (NDBI, Landsat 8) moderates the effect of routine repression on protest using ACLED event data, GADM Level 2 boundaries, and spatial econometrics (Moran's I, LISA, SAR/SEM). Preliminary cross-section: 395 districts.

## Paper

> Astuti, An Nisa. 2026. "Does Place Matter? The Geography of Repression and Mobilization in Indonesia." MACS 30200, Spring 2026.

## Repository structure

```
place-matters-indonesia/
├── eda_pipeline_v2_final.ipynb   # Main analysis pipeline
├── data/
│   ├── acled_classified_crosswalked.csv      # ACLED events, classified and crosswalked to GADM
│   ├── indonesia_ndbi_ndvi_2019.csv          # District-level NDBI/NDVI from GEE (Landsat 8, 2019)
│   ├── district_ndbi_repression_panel.csv    # Cross-section panel (395 districts)
│   └── gadm41_IDN_2.json                     # GADM Level 2 administrative boundaries
├── data/processed/
│   └── district_cross_section_v2.csv         # Final analytic cross-section (auto-generated)
├── figures/                                  # All figures used in the paper
├── requirements.txt
└── README.md
```

## Data sources

| Data | Source | Access |
|---|---|---|
| ACLED protest and repression events | [acleddata.com](https://acleddata.com) | Free registration required |
| Landsat 8 surface reflectance | [AWS Open Data Registry](https://registry.opendata.aws/usgs-landsat/) / Google Earth Engine | Public |
| GADM Level 2 boundaries | [gadm.org](https://gadm.org) | Free for non-commercial use |

**Note:** Raw ACLED data is not redistributed in this repository per ACLED terms of use. The classified and crosswalked derivative file (`acled_classified_crosswalked.csv`) is included. Raw Landsat imagery is not included due to size; it is available through the AWS Open Data Registry and Google Earth Engine.

## Reproducing the analysis

1. Clone this repository
2. Install dependencies: `pip install -r requirements.txt`
3. Run `eda_pipeline_v2_final.ipynb` sequentially from top to bottom
4. All figures are saved to `figures/` automatically

**Working directory:** The notebook sets `os.chdir()` at the top. Update this path to match your local environment before running.

## Key variables

| Variable | Operationalization | Source |
|---|---|---|
| Protest mobilization | Count of peaceful protest + violent demonstration events per district-year | ACLED |
| Routine repression | Count of protest with intervention events per district-year | ACLED |
| Lethal repression | Count of excessive force events with state-attributable fatalities | ACLED |
| NDBI | (SWIR1 - NIR) / (SWIR1 + NIR), dry-season median composite, April-October 2019 | Landsat 8 via GEE |
| NDVI | (NIR - Red) / (NIR + Red), same composite | Landsat 8 via GEE |

## Spatial weights

Queen contiguity + k-NN (k=3) hybrid, row-standardized. The k-NN component handles archipelagic districts that share no land borders.

## Citation

If you use this code or data, please cite the paper above and the original data sources.
