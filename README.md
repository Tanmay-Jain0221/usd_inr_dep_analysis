# INR–USD Depreciation: Structure vs Stress

This repository contains a historical, data-driven analysis of INR–USD depreciation, designed to distinguish between **long-run structural depreciation** and **episodic currency stress**.

The objective is not to forecast the exchange rate or identify short-term trading signals. Instead, the analysis places recent INR movements in historical context and evaluates whether current depreciation resembles past periods of genuine stress.

This work underpins an accompanying Substack post.

---

## Core Analytical Questions

The analysis is organised around four questions:

1. Is INR depreciation structurally persistent over long horizons?
2. How frequently does the rupee experience genuine currency stress?
3. Where does the latest INR depreciation sit relative to historical outcomes?
4. To what extent does long-run INR depreciation reflect India–US inflation differentials?

---

## Data Sources

All datasets used in this project are publicly available and sourced from official or widely used macroeconomic databases.

### Exchange Rate
- **USD–INR monthly averages**  
  Source: Investing.com  \
  https://in.investing.com/currencies/usd-inr-historical-data \
  Used to compute exchange rate levels and depreciation metrics.

### Inflation
- **India CPI (annual)**   
- **US CPI (annual)**  
  Source: World Bank\
  https://data.worldbank.org/indicator/FP.CPI.TOTL.ZG?locations=IN \
  Used to compute cumulative inflation differentials between India and the US.

### External Sector
- **India FX reserves (excluding gold)**  
  Source: IMF International Financial Statistics via FRED\
  https://fred.stlouisfed.org/series/TRESEGINM052N  \
  Used to measure reserve drawdowns and buffer pressure.

### Global Financial Conditions (Contextual)
- **US Dollar Index (DXY)**  
  Source: FRED  
- **US 10-year Treasury yields (nominal and real)**  
  Source: FRED  

Used for contextual interpretation only; not treated as primary stress drivers.

---

## Processed Data Files (What Each CSV Contains)

All raw data are cleaned, aligned, and standardised before analysis.  
No interpolation or forward-filling is used for stress identification metrics.

### `master_monthly.csv`
**Primary analysis dataset.**

Contains monthly observations of:
- `date`
- `fx_rate` (USD–INR monthly average)
- `inr_dep_12m` (YoY INR depreciation, %)
- `fx_logret` (log returns of USD–INR)
- `fx_vol_12m` (12-month rolling FX volatility, annualised)
- `fx_reserves` (level)
- `reserves_12m_change` (YoY % change in reserves)
- selected global context variables (DXY, US 10Y yields)

Used for:
- stress regime identification
- stress episode construction
- Charts 1, 2, and 3

---

### `master_yearly.csv`
**Structural / long-run dataset.**

Contains annual series of:
- `year`
- `cum_inr_dep` (cumulative INR depreciation, indexed to base year)
- `cum_inflation_diff` (cumulative India–US inflation differential)

Used exclusively for:
- long-run structural comparison (Chart 4)

---

### Supporting Source Files

- `usd_inr_avg_monthly.csv`  
  Clean monthly USD–INR averages (base exchange rate series).

- `india_cpi_yearly.csv`  
  Annual CPI inflation for India.

- `us_cpi_yearly.csv`  
  Annual CPI inflation for the United States.

- `fx_reserves_india_monthly.csv`  
  Monthly FX reserves for India (excluding gold).

- `dxy_avg_monthly.csv`  
  Monthly average US Dollar Index.

- `us10y_nominal_avg_monthly.csv`  
  Monthly nominal US 10-year Treasury yield.

- `us10y_real_avg_monthly.csv`  
  Monthly real US 10-year Treasury yield.

---

## Methodological Framework

### Depreciation vs Stress

INR depreciation is treated as a **continuous structural process**.  
Currency stress is treated as a **regime**, not a smooth gradient.

Stress is not defined by depreciation alone.

---

### Stress Metrics (Notebook-Aligned)

Stress identification uses three dimensions derived from `master_monthly.csv`:

- **Depreciation pace:** `inr_dep_12m`
- **FX volatility:** `fx_vol_12m`
- **Reserve dynamics:** `reserves_12m_change`

Thresholds are defined using historical percentiles rather than fixed levels.

---

### Stress Regime Classification

Monthly observations are classified into three regimes:

- **Normal depreciation**
- **Elevated pressure**
- **Stress episode**

Stress episodes require clustering of extreme depreciation pace together with elevated volatility and/or reserve drawdowns.  
Elevated pressure captures faster depreciation combined with rising volatility or mild reserve erosion, subject to persistence filters.

---

### Episode Construction

Stress months are grouped into **episodes** based on temporal continuity.

Each episode is summarised by:
- start and end date
- duration (months)
- peak YoY depreciation (`peak_dep`)
- peak FX volatility
- worst reserve drawdown

This episode-based approach avoids over-interpreting isolated monthly moves.

---

### Structural Anchor

To explain why INR depreciation persists outside stress regimes, the analysis compares:
- cumulative INR depreciation (`cum_inr_dep`), and
- cumulative India–US inflation differentials (`cum_inflation_diff`).

This provides a slow-moving structural benchmark against which episodic shocks can be evaluated.

---

## Repository Structure



## Repository Structure

```
│
├── data/
│ ├── processed/
| | ├── inr_stress_test.csv
│ │ ├── master_monthly.csv
│ │ └── master_yearly.csv
│ ├── cleaned/ 
| | ├── dxy_avg_monthly.csv    
| | ├── fx_reserves_india_monthly.csv
| | ├── india_cpi_yearly.csv    
│ | ├── us10y_nominal_avg_monthly.csv
│ | ├── us10y_real_avg_monthly.csv
│ | ├── us_cpi_yearly.csv
│ | └── usd_inr_avg_monthly.csv
│ ├── raw/  
│ | ├── dxy_rate_1985-2025.csv
| | ├── forex_reserves_1950-2025.csv
| | ├── fx_rate_1985-2025.csv    
│ | ├── inflation_ind_us.csv
│ | ├── us_10y_yield_nominal.csv
│ | ├── us_10y_yield_real.csv
| └─└── worldbank_inflation_rate_1985-2024.csv
|
├── figures/
│ ├── chart1_usd_inr_stress.png
│ ├── chart2_distribution.png
│ ├── chart3_stress_episodes.png
│ └── chart4_inflation_anchor.png
|
├── notebooks/
│ └── inr_fx_analysis.ipynb
|
├── README.md
└── requirements.txt
```

---

## Scope and Limitations

- This is a **descriptive**, not predictive, analysis.
- No econometric estimation or causal attribution is attempted.
- Short-term flow dynamics and positioning are not modelled.
- The framework prioritises interpretability, robustness, and historical context.

---

## Intended Use

This repository is intended for:
- readers interested in historical currency behaviour,
- analysts evaluating INR risk through regimes rather than spot levels,
- practitioners seeking a transparent, rule-based stress framework.

---


### Note: The code is MIT-licensed. The written analysis and narrative interpretation are not intended for commercial reuse without permission.
