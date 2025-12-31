# INR–USD Depreciation: Stress vs Structure

This repository contains a data-driven analysis of long-run INR–USD depreciation, with a focus on distinguishing
between **structural depreciation** and **episodic currency stress**.

The goal is not to forecast the exchange rate, but to place recent INR moves in historical context and assess
whether current depreciation reflects abnormal stress or historical norms.

## Key Questions Addressed

- Is INR depreciation structurally persistent over time?
- How rare are true currency stress episodes?
- Where does the latest INR depreciation sit relative to history?
- How closely does long-run INR depreciation track the India–US inflation differential?

## Methodology

- Monthly USD–INR data (Apr 1985 - Dec 2025)
- YoY depreciation, rolling FX volatility, and FX reserve changes
- Stress regimes identified using a composite, rule-based framework
- Stress episodes grouped and analyzed by duration and severity
- Inflation differential used as a long-run structural anchor

## Key Findings

- INR depreciates structurally over long horizons.
- Median YoY depreciation is modest relative to crisis periods.
- True stress episodes are rare and clustered.
- Recent depreciation remains well below historical stress thresholds.
- Over decades, INR depreciation broadly reflects inflation arithmetic.

## Repository Contents

- `notebooks/inr_fx_analysis.ipynb` – full analysis and chart generation
- `data/processed/` – cleaned monthly and yearly datasets
- `figures/` – final charts used in the accompanying Substack post

## Notes

This project is intended for analytical and educational purposes.
It avoids econometric overfitting and focuses on clarity, robustness, and historical context.
