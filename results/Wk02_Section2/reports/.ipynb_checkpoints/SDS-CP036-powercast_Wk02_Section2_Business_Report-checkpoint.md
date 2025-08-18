# Week 2 — Section 2: Lag and Rolling Statistics

**Dataset:** `Tetuan City power consumption.csv`
**Period: 2017-01-01 00:00:00 → 2017-12-30 23:50:00 | Rows: 52416 | Median step: 600 seconds**

1. Lag and Rolling Statistics
Q: How did you determine which lag features and rolling statistics (mean, std, median, etc.) to engineer for each zone?
A: We aligned the feature windows with real-world usage rhythms. Based on the data’s median sampling step, we built lags at one step (immediate past), about 1 hour, and about 24 hours, and rolling windows of ~1, ~3, and ~24 hours for mean, standard deviation, and median. This mirrors short-term reaction, intra-day trends, and daily cycles that typically drive demand across zones.

Q: What impact did lag and rolling features have on model performance or interpretability?
A: Against a simple mean baseline, lag features reduced error vs. a flat-mean baseline by ~88.6%; rolling(1h) features improved error by ~81.4% vs. mean. The rolling windows also make patterns more interpretable by smoothing noise and highlighting typical intra-day levels (~1 hour, ~3 hours, ~24 hours). See the MAE comparison bar chart.

Q: How did you handle missing values introduced by lag or rolling computations?
A: Lags and rolling windows naturally create missing values at the start of the series. We kept those missing values in the raw engineered file for transparency, and also produced an imputed copy using forward-fill, backfill, and then median fill where needed. This keeps downstream modeling simple without distorting early observations.

## Artifacts
- Engineered dataset (raw): `features/engineered_lag_rolling.csv`
- Engineered dataset (imputed): `features/engineered_lag_rolling_imputed.csv`
- Plots: ['wk02_section2_rolling24_overlay.png', 'wk02_section2_baseline_mae.png']
- Machine-readable summary: `summary.json`