---
name: latency-percentile-analysis
version: 1.0.0
description: >
  Analyse latency and other skewed timings with percentiles, correct aggregation, segments and coverage of failed requests. Use when summarising performance data or comparing before and after speed.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - performance
  - statistics
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: latency-percentile-analysis
  official: true
  domain: data
  security_flags: []
---

# Latency Percentile Analysis

## When to use
You have request or job durations and need to say how slow things are or whether a change helped.

## Steps
1. Establish what each duration covers (client, edge or server; queue time included or not) and its units.
2. Check how timeouts, errors and cancellations are recorded. Dropping them removes the slowest cases; report their rate beside latency.
3. Plot the distribution, preferably on a log axis, and look for several peaks or a spike at a timeout value.
4. Report count, p50, p95 and p99. Add p99.9 only when there are enough samples that it is not one or two points.
5. Compute percentiles from raw values or mergeable histograms or sketches. Never average per-minute or per-host percentiles.
6. For histogram data, check bucket boundaries around the values of interest, since quantiles are interpolated within buckets.
7. Segment by endpoint, payload size, region, cache hit or miss and cold start.
8. Compare before and after over matched traffic mix and time of day, with bootstrap intervals or several repeated windows.
9. For load tests, check whether the generator waits for responses before sending more. That hides queueing delay (coordinated omission); use a fixed arrival rate.
10. Estimate user impact: a page making many calls hits tail latency far more often than any single call does.

## Watch out for
- A better p50 can hide a worse p99.
- Fast failures make latency look better during an outage.
- Sampled traces biased toward slow or failed requests cannot give population percentiles.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Figures state measurement point, sample count and error rate, and any claimed improvement holds on comparable traffic.
