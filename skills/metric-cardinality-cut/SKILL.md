---
name: metric-cardinality-cut
version: 1.0.0
description: >
  Find the metrics and labels driving time series explosion in Prometheus-style monitoring and reduce them safely. Use when the metrics store runs out of memory or the monitoring bill jumps.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - observability
  - cost
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - edit
metadata:
  source: library
  library_id: metric-cardinality-cut
  official: true
  domain: ops
  security_flags: []
---

# Metric Cardinality Cut

## When to use
Series counts or ingestion cost are growing faster than the systems being monitored.

## Steps
1. Measure total active series and their trend. In Prometheus, read the TSDB status page or `/api/v1/status/tsdb` for the top metric names and labels.
2. Break down heavy metrics with `count by (job) (metric_name)`. A global `count by (__name__) ({__name__!=""})` is expensive, so avoid it on a struggling server.
3. For the worst metric, count distinct values per label to find the culprit: user or request IDs, raw URL paths, error text, pod names that churn, timestamps.
4. Check where it is used: dashboards, alert rules, recording rules and ad hoc queries from query logs.
5. Prefer fixing at the source: use route templates instead of paths, bounded error classes, and move per-request detail to traces or logs.
6. Review histograms; series multiply by bucket count times every label combination.
7. As a stopgap, use `metric_relabel_configs` to drop whole metrics or unused buckets, validating with `promtool check config`.
8. Add per-target sample limits and an alert on series growth.
9. Compare series count and affected queries after the old series age out.

## Watch out for
- `labeldrop` can make distinct series collide into identical ones, causing duplicate-sample errors and wrong values. Aggregate at the source instead.
- Dropping histogram buckets that include `+Inf` breaks quantiles.
- A sample limit rejects the entire scrape when exceeded, so set headroom.
- Memory does not fall immediately after a change.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Active series are measurably lower, no dashboard or alert lost required data, and the offending label cannot silently return.
