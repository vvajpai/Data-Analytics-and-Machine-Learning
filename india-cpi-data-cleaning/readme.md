# India CPI Data Cleaning

Cleaning and preparing the India Consumer Price Index dataset (2014–2025):
handling missing values, disguised zeros, and structural gaps.

## Dataset
- ~292k rows, monthly CPI by state × commodity group × sector (2014–2025).
- Source: <link/attribution>

## Problem
- `cpi` & `inflation_rate` had ~1% missing values...
- ...plus **8,360 disguised missing values encoded as `0`** (a CPI of 0 is impossible).

## Approach
1. Detected disguised missing (`0` → `NaN`) via range/`describe()` checks.
2. Classified **structural** (never measured, e.g. rural Housing) vs **fillable** gaps.
3. Dropped structural series; **time-interpolated** 39 interior gaps within each series.
4. Repaired corrupted `inflation_rate` and validated (0 missing, no impossible values).

## Key decisions
- Rural Housing dropped — India doesn't compile rural housing CPI (0 real values).
- Arunachal Pradesh Urban/Combined dropped — never measured (mostly rural state).
- Interior gaps (mostly COVID-era Apr–Jun 2021) interpolated, not deleted.

## Results
- Final: 280,592 clean rows, 0 missing, 0 impossible values.
