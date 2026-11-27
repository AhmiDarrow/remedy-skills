---
name: time-series-forecast-baseline
version: 1.0.0
description: >
  Forecast a metric with naive and seasonal baselines, rolling-origin backtests and honest uncertainty ranges. Use when asked to predict demand, traffic, volume or similar series.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - forecasting
  - statistics
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: time-series-forecast-baseline
  official: true
  domain: data
  security_flags: []
---

# Time Series Forecast Baseline

## When to use
Someone needs future values of a time series for planning.

## Steps
1. Ask what decision the forecast serves, the horizon, the grain, and whether over- or under-prediction costs more.
2. Rebuild the series on a complete time index. Distinguish zero from missing, drop the partial last period, and handle daylight-saving effects for sub-daily data.
3. Plot it and annotate outages, promotions, launches, definition changes and holidays. Note whether history reflects demand or a capacity limit such as stockouts.
4. Create baselines: last value, seasonal naive (same weekday or month last cycle), and a simple trend or moving average.
5. Backtest with rolling origins: train up to a cutoff, forecast the real horizon, advance and repeat.
6. Score with MAE and bias, and a scaled error such as MASE. Avoid MAPE when values are near zero.
7. Try exponential smoothing, ARIMA or a regression with calendar features, and keep one only if it beats the best baseline across folds.
8. Use only inputs that will be known at forecast time; future weather or traffic must itself be forecast.
9. Derive intervals from backtest errors by horizon and check how often actuals fell inside.
10. Deliver the forecast with range, assumptions, backtest error and a date to compare against actuals.

## Watch out for
- Random train-test splits leak the future.
- With under two full seasonal cycles, yearly seasonality cannot be estimated reliably.
- Long horizons from short histories mostly extrapolate recent noise; say so.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The chosen method is shown against a baseline on rolling backtests, and the output includes calibrated or clearly caveated ranges.
