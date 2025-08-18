# Week 2 — Section 3: Feature Scaling & Normalization

**Dataset:** `Tetuan City power consumption.csv`
**Period: 2017-01-01 00:00:00 → 2017-12-30 23:50:00 | Rows: 52416 | Median step: 600 seconds**

## Key Questions Answered
### 3. Feature Scaling & Normalization
Q: Which normalization or scaling techniques did you apply to your numerical features, and why?
A: We applied three well-known scaling approaches to the numerical features:
- **Standardization (z-score):** Centers each feature at 0 and scales by its typical spread (standard deviation). This is a good default when values look roughly bell-shaped.
- **Min–Max scaling:** Compresses values to a 0–1 range so features are on the same scale, useful for models sensitive to feature range.
- **Robust scaling:** Centers using the median and scales using the interquartile range (IQR). This is more resistant to outliers and skew.
Using all three gives flexibility: teams can pick the scaler that best fits their downstream model and operational needs.

Q: How did you ensure that scaling was performed without introducing data leakage?
A: To prevent **data leakage** (accidentally using future information), we split the data by time first (earliest → latest) and **fit** each scaler on the **training** portion only. We then **applied** the learned scaling to the held-out test period. This mirrors how the model will see data in production and keeps evaluation honest.

Q: Did you notice any features that required special treatment during normalization?
A: We intentionally **left some features unscaled** because they are binary flags or already unitless encodings: is_weekend_x, is_weekend_y. Cyclical encodings (e.g., sin/cos of hour or day) are already normalized between –1 and 1. If a feature showed heavy skew or outliers, **Robust scaling** is preferred to avoid undue influence.

## Artifacts
- Scaled features (Standard): `features/scaled_standard_train.csv`, `features/scaled_standard_test.csv`
- Scaled features (MinMax): `features/scaled_minmax_train.csv`, `features/scaled_minmax_test.csv`
- Scaled features (Robust): `features/scaled_robust_train.csv`, `features/scaled_robust_test.csv`
- Scaler parameters: `features/scalers.json`
- Plots: ['standard_Temperature_before.png', 'standard_Temperature_after.png']
- Machine-readable summary: `summary.json`