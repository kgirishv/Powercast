# Week 2 — Section 4: Data Splitting & Preparation

**Primary input:** `scaled_standard_train.csv + scaled_standard_test.csv`
**Rows: 52416 | Train rows: 41932 | Test rows: 10484 | Target: Total_auto**

## Key Questions Answered
### 4. Data Splitting & Preparation
Q: How did you split your data into training and test sets to maintain chronological order?
A: We kept the natural **chronological order**. If Section 3 train/test files were available, we reused them as-is. Otherwise, we created an **80/20 time split** (earliest → latest) with **no shuffling**, which mirrors how new data arrives in production.

Q: What steps did you take to prevent information leakage between splits?
A: To prevent **information leakage**—future data affecting training—we ensured that any learned settings (e.g., scalers upstream) were **fit on training only** and then **applied to test**. We also avoided look‑ahead features when constructing targets and respected the time boundary.

Q: How did you verify that your train/test split was appropriate for time-series forecasting?
A: We verified the split with a simple **walk‑forward check** and a **timeline plot**. The walk‑forward step evaluates a naïve baseline (lag‑1) across rolling folds; stable errors across folds and a clean split marker in the plot indicate the split is appropriate for time‑series forecasting.

## Artifacts
- Train: `features/train.csv`
- Test: `features/test.csv`
- Walk-forward results: `features/walk_forward_results.csv`
- Plot: `wk02_section4_split_marker.png`
- Machine-readable summary: `summary.json`