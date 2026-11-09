# Forest structure and vertical microclimate

Reproducible analysis materials for the study **“Using forest structural complexity and topography metrics to characterise vertical microclimatic stratification.”** The repository brings together sensor and environmental data, data-preparation scripts, statistical models, model outputs, figures, and diagnostics used in the study.

> **Publication:** Sébastien Lhoumeau, Dominik Seidel, Rui B. Elias, Rosalina Gabriel, and Paulo A. V. Borges (2026). *Ecological Informatics*, 99, 104087. [https://doi.org/10.1016/j.ecoinf.2026.104087](https://doi.org/10.1016/j.ecoinf.2026.104087)

## What is here

- **`code/`** — numbered Python, Julia, and R scripts for solar-radiation acquisition and formatting, sensor-data preparation and quality correction, data compilation and visualization, model fitting, and correlation figures.
- **`data/`** — microclimate time series and corrected summaries, compiled modelling data, Copernicus-derived radiation data, LiDAR/vegetation structure data, site locations, and model estimates/significant interaction tables.
- **`docs/`** — figures, data-logger time-series visualizations, model diagnostics, supplementary files, and a model-validation workbook.
- **`Project.toml` and `Manifest.toml`** — Julia project dependencies and a locked Julia environment.

The repository includes a prepared modelling table at `data/microclimate_data/data_modelling.csv` as well as upstream data and intermediate outputs. The modelling script uses canopy openness, foliage-height diversity, LiDAR structural-complexity metrics, elevation, slope, and aspect-derived northness/eastness as predictors. It evaluates 12 microclimate response variables across ground, understory, and canopy strata, including temperature and vapour-pressure-deficit means and daily ranges. The R analysis also includes seasonality terms and examines interactions between solar energy and structural/topographic predictors.

## Analysis workflow

The numbered scripts in `code/` document the analysis workflow:

1. **Acquire and prepare solar-radiation data** — `01-1-solar_radiation_copernicus_dwld.py` requests hourly CAMS solar-radiation time series; `01-2-formatting_copernicus_data.jl` formats the downloaded data.
2. **Prepare sensor observations** — `02-data_daily computation.jl`, `03-1-Correct_outlier_data.R`, and `03-2-Visualise_time_series_datalogger.R` cover daily computation, outlier correction, and logger-series visualization.
3. **Compile analysis data** — `04-data_compilation.jl` combines daily microclimate summaries, radiation, and vegetation structure into the modelling dataset.
4. **Describe and model** — `05-data_description_visualisation.R` explores the data; `06-Stratum_models_fit.R` fits stratum-specific models and exports estimates, interaction tables, validation results, and diagnostics.
5. **Visualize correlations** — `07-HeatMap_correlation_figure.R` produces correlation heatmaps.

This ordering describes the script roles, not a guarantee that every script can be run unchanged from the repository root: the scripts expect particular input paths and some upstream raw inputs or services may need to be configured. Inspect the input/output paths in each script before running it.

## Software and external access

- **Julia** is used for radiation formatting and data preparation/compilation. The repository provides `Project.toml` and `Manifest.toml`; activate the project environment before running Julia scripts.
- **R** is used for data correction, visualization, and modeling. `code/00-R_package_loader.R` loads the R packages used by the analysis (including `tidyverse`, `nlme`, `lme4`, `glmmTMB`, and `writexl`) via `pacman`.
- **Python** is used by the CAMS download script, which imports `cdsapi` and `pandas`. Its comments state that CAMS API credentials are required to connect to the Copernicus Climate Data Store. See the [CAMS API instructions](https://cds.climate.copernicus.eu/how-to-api).

The Julia project file does not describe the R or Python environments; those dependencies must be installed separately.

## Results and supporting material

- Model estimates and interaction summaries are available as CSV files in `data/`, including seasonal and non-seasonal variants.
- Model validation and diagnostics are in `docs/model_validation.xlsx`, `docs/diagnostics/`, `docs/diagnostics_V2/`, and `docs/supplementary/`.
- Figures are in `docs/Figures/` and supplementary figures/materials in `docs/supplementary/`.

## Citation

Lhoumeau, S., Seidel, D., Elias, R. B., Gabriel, R., & Borges, P. A. V. (2026). Using forest structural complexity and topography metrics to characterise vertical microclimatic stratification. *Ecological Informatics, 99*, 104087. [https://doi.org/10.1016/j.ecoinf.2026.104087](https://doi.org/10.1016/j.ecoinf.2026.104087)
