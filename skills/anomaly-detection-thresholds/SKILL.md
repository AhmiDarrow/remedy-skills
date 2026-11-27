---
name: anomaly-detection-thresholds
version: 1.0.0
description: >
  Set metric anomaly alerts that respect seasonality and volume, tuned by replaying past incidents. Use when static thresholds fire constantly or miss real problems in business or data metrics.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - monitoring
  - statistics
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: anomaly-detection-thresholds
  official: true
  domain: data
  security_flags: []
---

# Anomaly Detection Thresholds

## When to use
A series needs automatic flagging of unusual values.

## Steps
1. Define what should wake someone, how quickly, and what they would do. A series with no action needs no alert.
2. Collect history and a list of known incidents and known harmless spikes.
3. Characterize it: daily and weekly cycles, trend, holidays, typical volume, data arrival delay.
4. Start simple: compare with the same hour and weekday over recent weeks, using the median and median absolute deviation so past outliers do not widen the band. Keep a hard floor or ceiling for impossible values.
5. For ratios, require a minimum denominator or use a binomial-based interval.
6. Evaluate only complete buckets, allowing for observed lateness.
7. Require persistence or two windows for noisy series, and add a separate slow-drift check comparing longer windows, since a rolling baseline absorbs gradual decline.
8. Replay history. For each configuration count caught incidents, missed ones, false alerts per week and detection delay, then show the trade-off to the owner.
9. Make the alert show observed value, expected range, affected segments and a link or query.
10. Alert separately on missing data. Exclude confirmed incidents from future baselines, and review thresholds after real firings.

## Watch out for
- Monitoring hundreds of segments produces false alarms by chance alone; limit or adjust.
- A three-sigma rule assumes a distribution many metrics do not have.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Replay results are recorded for the chosen settings, an injected drop fires within the target delay, and each alert names an owner and first action.
