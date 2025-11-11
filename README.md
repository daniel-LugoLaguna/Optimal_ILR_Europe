# Optimal ILR in Utility-Scale PV Plants Across Europe

The project quantifies the techno-economic optimization of DC oversizing (Inverter Loading Ratio, ILR) in utility-scale photovoltaic (PV) plants across European capitals, integrating minute-resolution energy production data with country-specific financial parameters.

---

## Repository Overview

| Folder | Description |
|--------|--------------|
| **`notebooks/`** | Jupyter notebooks containing all computational steps, from irradiance data retrieval to financial analysis and figure generation. |
| **`data/`** | Core simulation outputs and derived economic results (CSV files). Large intermediate irradiance time-series are not included due to size constraints (>9 GB). |

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
## Financial parameters and discount-rate

In order to make the techno-economic comparison across European capitals transparent, the repository includes the country-level inputs used to compute the discount rate (DR) / WACC applied in the simulations.

The file **`data/Discount_rate_estimation.csv`** contains, for each country:

- `country` – ISO/country name used in the simulations
- `MRP` – Market Risk Premium used for the country (%)
- `RRF` – Risk-free rate / 10-year sovereign reference rate (%)
- `CRP` – Country Risk Premium added to reflect sovereign/country exposure (%)
- `levered_beta` – Sectoral levered beta adopted for PV/infrastructure
- `DP` – Debt premium / corporate spread (%)
- `Ti` – Corporate income tax rate (%)
- `spread` – Additional project/regulatory spread (0.5% in the paper) (%)
- `Re` – Cost of equity after applying CAPM (%)
- `Rd` – Cost of debt after tax shield (%)
- `WACC` – Weighted Average Cost of Capital, after tax (%)
- `DR` – Final discount rate used in the cash-flow model (%)

**Important:** in the notebooks we only load the **final** discount rate (`DR`) for each country to keep the code compact.  
The **full derivation** of these values — CAPM, debt leg, tax effect and final spread — is documented in the manuscript, where every intermediate step is explained and referenced.

This separation (CSV with inputs + explanation in the paper) allows:
1. reproducibility of the numerical results,
2. traceability of financial assumptions, and
3. future updates of country-specific financial conditions without modifying the modeling code.

---
## Data sources

The modeling framework integrates high-resolution irradiance, meteorological, and component performance data from open-access scientific repositories.

### Solar irradiance data
Irradiance inputs were obtained from the **Copernicus Atmosphere Monitoring Service (CAMS)** via the Atmosphere Data Store:

> [CAMS Solar Radiation Service – Time Series](https://ads.atmosphere.copernicus.eu/datasets/cams-solar-radiation-timeseries?tab=download)

CAMS provides hourly and sub-hourly solar radiation data derived from satellite observations and reanalysis models, distributed under the **Copernicus Data Licence**.  
All irradiance datasets were downloaded for the coordinates of each European capital and processed using the notebooks  
`1_load_city_files.ipynb` and `2_calculate_city_energy.ipynb`.

### Meteorological data
Complementary meteorological variables — including ambient temperature, wind speed, and relative humidity — were retrieved through the **Open-Meteo API**, an open-access service:

> [Open-Meteo API](https://open-meteo.com/en/docs)

These data were used to parameterize module temperature and inverter efficiency models, ensuring consistency between irradiance and environmental conditions for each site.

### PV module and inverter specifications
Technical characteristics of the PV modules and inverters were obtained from the **NREL System Advisor Model (SAM)** public database, which provides standardized performance parameters for commercially available technologies:

> [NREL/SAM Technology Database – GitHub Repository](https://github.com/NREL/SAM/tree/develop)

The following components were used throughout the simulations:

- **PV module:** *Chint New Energy Technology Co., Ltd. — CHSM66M-DG(FBH)-635*  
- **Inverter:** *Chint Power Systems America — CPS SCH350KTL-DO/US-800 (800 V)*  

These devices were selected as representative of modern utility-scale equipment and are included in the **CEC (California Energy Commission) database** integrated in **NREL/SAM** and **pvlib-python**.

### PV modeling library
PV system performance was simulated with **pvlib-python**, an open-source library for photovoltaic system modeling:

> [pvlib-python documentation](https://pvlib-python.readthedocs.io/en/stable/)

pvlib was used to load CEC module and inverter parameters, compute plane-of-array irradiance, apply temperature models, and evaluate AC power at one-minute resolution.

### Data reproducibility
Due to their size (≈9 GB), the raw time-series of irradiance and meteorological data are **not included** in this repository.  
However, all datasets can be **fully reproduced** by users with a free CAMS and Open-Meteo account, following the workflow in the notebooks above.  
Derived results and processed data — including annual energy yields, clipping ratios, and financial indicators — are provided as CSV files in the `data/` directory.

---
