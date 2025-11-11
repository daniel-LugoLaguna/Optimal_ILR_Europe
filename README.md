# Optimal ILR in Utility-Scale PV Plants Across Europe

The project quantifies the techno-economic trade-offs of DC oversizing (Inverter Loading Ratio, ILR) in utility-scale photovoltaic (PV) plants across European capitals, integrating minute-resolution irradiance data with country-specific financial parameters.

---

## 🔍 Repository overview

| Folder | Description |
|--------|--------------|
| **`notebooks/`** | Jupyter notebooks containing all computational steps, from irradiance loading to financial analysis and figure generation. |
| **`data/`** | Core simulation outputs and derived economic results (CSV files). Large intermediate irradiance and energy time-series files are not included due to size constraints (>20 GB total). |
| **`docs/`** | Additional documentation or figures used in the manuscript. |

---

## ⚙️ Workflow summary

1. **`1_carga_ficheros_ciudades_FV.ipynb`** – Loads minute-resolution irradiance and temperature data for each capital and prepares PV system inputs.
2. **`2_calculo_produccion_ciudades_FV.ipynb`** – Calculates hourly and annual PV generation for a range of ILR values using the defined plant model.
3. **`3_calcula_clipping_FV.ipynb`** – Determines inverter clipping losses and computes effective AC yield.
4. **`4_analisis_economico.ipynb`** – Combines energy results with cost, PPA, and discount rate assumptions to estimate NPV/I for each configuration.
5. **`graficos_comparison_ILR.ipynb`** – Generates comparative plots of optimal ILR values, profitability maps, and sensitivity analyses.

---

## 📂 Available datasets

| File | Description |
|------|--------------|
| `all_cities_all_ILR_energy.csv` | Annual energy yield (AC) for each city and ILR configuration. |
| `ilr_costs_by_city.csv` | CAPEX, OPEX, and discount rate assumptions per country. |
| `financial_results_parametric.csv` | Sensitivity results varying module costs and PPA prices. |
| `optimal_ilr_by_country_all_scenarios.csv` | Summary of optimal ILR values under different financial and technical conditions. |

Large intermediate datasets (minute-level irradiance and DC output per city) are **not uploaded** due to storage limits. However, these files can be **reproduced** directly using the first two notebooks and the public meteorological databases specified in the manuscript.

---
