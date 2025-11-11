# Optimal ILR in Utility-Scale PV Plants Across Europe

The project quantifies the techno-economic trade-offs of DC oversizing (Inverter Loading Ratio, ILR) in utility-scale photovoltaic (PV) plants across European capitals, integrating minute-resolution irradiance data with country-specific financial parameters.

---

## Repository Overview

| Folder | Description |
|--------|--------------|
| **`notebooks/`** | Jupyter notebooks containing all computational steps, from irradiance data retrieval to financial analysis and figure generation. |
| **`data/`** | Core simulation outputs and derived economic results (CSV files). Large intermediate irradiance time-series are not included due to size constraints (>20 GB). |
| **`docs/`** | Additional documentation and supporting figures used in the manuscript. |

---

## Workflow Summary

1. **`1_load_city_files.ipynb`** – Retrieves and formats irradiance and temperature data for each capital.
2. **`2_calculate_city_energy.ipynb`** – Computes DC and AC generation for a range of ILR values.
3. **`3_calculate_clipping.ipynb`** – Estimates inverter clipping losses and effective energy yield.
4. **`4_economic_analysis.ipynb`** – Combines energy results with cost, PPA, and discount rate data to estimate profitability (NPV/I).
5. **`5_generate_figures.ipynb`** – Produces all comparative plots and maps included in the publication.

---

## Available datasets

| File | Description |
|------|--------------|
| `all_cities_all_ILR_energy.csv` | Annual energy yield (AC) for each city and ILR configuration. |
| `ilr_costs_by_city.csv` | CAPEX, OPEX, and discount rate assumptions per country. |
| `financial_results_parametric.csv` | Sensitivity results varying module costs and PPA prices. |
| `optimal_ilr_by_country_all_scenarios.csv` | Summary of optimal ILR values under different financial and technical conditions. |

---
## ☀️ Data sources

The irradiance and meteorological inputs used in this study were obtained from the **Copernicus Atmosphere Monitoring Service (CAMS)** through the Atmosphere Data Store:

> [CAMS Solar Radiation Service – Time Series](https://ads.atmosphere.copernicus.eu/datasets/cams-solar-radiation-timeseries?tab=download)

CAMS provides hourly and sub-hourly solar radiation data derived from satellite observations and reanalysis models, available under the **Copernicus Data Licence**.  
All irradiance datasets were retrieved for the coordinates of each European capital and processed using the notebooks `1_carga_ficheros_ciudades_FV.ipynb` and `2_calculo_produccion_ciudades_FV.ipynb`.  

Due to their large size (≈9 GB), these time-series are **not included in the repository**, but can be **fully reproduced** by users with a Copernicus account (free access after registration).

---
