# Forecasting International Cocoa Prices (1994–2025)

**What this is.** A reproducible R/R Markdown project that forecasts international cocoa prices using multiple time-series families: **ETS**, **ARIMAX/SARIMAX**, **ARIMA + GARCH**, and a baseline **multiple linear regression** with climate regressors. We aggregate daily series to monthly, compare models out-of-sample (Aug–Nov 2024), and discuss volatility and structural breaks.

**Why it matters.** Cocoa prices are volatile and climate-sensitive. We test whether adding Ghana climate variables improves short-run forecast accuracy over standard univariate models and whether volatility models (GARCH) better handle the 2023–2024 surge.

---

## Data (sources & scope)
- **Prices:** International cocoa futures, monthly aggregation (1994–2025).
- **Climate (Ghana):** Monthly PRCP, TAVG, TMAX, TMIN aligned to price series.
- **Frequency:** Monthly; train: 1994-11–2024-07; test: 2024-08–2024-11.

> Raw data are **not** distributed. See `data/README.md` for download links, expected filenames, and where to place them.

---

## Methods (one-page tour)
- **ETS(A,N,N)** on differenced series for level dynamics.
- **ARIMAX / SARIMAX** with monthly seasonality and exogenous climate regressors.
- **ARIMA + GARCH(1,1)** to capture volatility clustering.
- **Multiple Linear Regression** with time trend + climate variables.
- Evaluation with RMSE/MAE/MAPE; visual forecast vs actual comparisons.

---

## Repo structure
  analysis/ # cocoa_forecasting.Rmd (main analysis)
  docs/ # paper.pdf (write-up)
  data/ # raw/ and processed/ (both gitignored), plus README.md
  results/ # figures/ and tables/ exported by the Rmd
  code/ # optional modular R scripts


---

## How to reproduce

1. Setup
  - **R** ≥ 4.3 and (optional) RStudio.
  - Install required packages:
  ```r
  pkgs <- c("tidyverse","lubridate","forecast","tseries","fGarch","rugarch","readr","readxl","xts","zoo","ggplot2")
  to_install <- setdiff(pkgs, rownames(installed.packages()))
  if(length(to_install)) install.packages(to_install)
  ```


2. Put data in place
  Follow data/README.md. Ensure filenames/paths match what the Rmd expects (see header chunk).

3. Knit
  Open analysis/cocoa_forecasting.Rmd and Knit to HTML or PDF.
  Artifacts are written to results/figures/ and results/tables/.
  
## Results at a glance
  results/figures/ — comparative forecast plots (ETS vs ARIMAX/SARIMAX vs GARCH vs MLR).
  
  results/tables/ — accuracy metrics (RMSE/MAE/MAPE) and selected parameter summaries.
  
  TL;DR. GARCH(1,1) handled volatility best and delivered the lowest test-set errors; climate regressors were limited for short-run prediction during the 2023–2024 surge.
