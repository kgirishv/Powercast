# Week 2 — Section 1: Time-Based Feature Engineering

**Dataset:** `Tetuan City power consumption.csv`
**Period:** 2017-01-01 00:00:00 → 2017-12-30 23:50:00
**Rows:** 52416
**Median sampling step:** 600 seconds

1. Time-Based Feature Engineering
Q: Which time-based features did you create (e.g., hour, weekday, weekend, month), and why did you select them?
A:
- Calendar: hour, weekday (0=Mon), weekend flag, month, quarter, day, ISO week, day-of-year.
- Cyclical encodings (sin/cos) for hour, weekday, day-of-year to preserve periodicity and avoid 23→0 wrap-around.

Q: How did these new features help capture patterns in power consumption?
A:
- hourly profile shows a peak near **20:00**; weekday profile peaks on **Thu**; cyclical encodings improve linear models' ability to learn smooth periodic effects.

Q: Did you encounter any challenges when extracting or encoding time features? How did you address them?
A:
- Robust timestamp parsing with day-first fallback;
- Inferred cadence from median step; flagged potential irregularities;
- Used cyclical encoding to represent circular time dimensions.

## Artifacts
- Engineered dataset: `features/engineered_time_features.csv`
- Plots: ['wk02_section1_hourly_profile.png', 'wk02_section1_dayofweek_profile.png']
- Machine-readable summary: `summary.json`