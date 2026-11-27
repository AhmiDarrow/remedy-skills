---
name: metrics-instrumentation
version: 1.0.1
description: >
  Add service metrics for traffic, errors, latency and resource saturation with correct types, units and bounded labels. Use when a service has no dashboards or alerts to tell if it is healthy.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - observability
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: metrics-instrumentation
  official: true
  security_flags: []
---

# Metrics Instrumentation

## When to use
Code needs measurements that can answer operational questions over time.

## Steps
1. Find the metrics library, naming conventions, exporter and metrics already emitted by the framework, so nothing is counted twice.
2. List the questions: are users succeeding, how slow is it, what is close to full? Cover rate, errors and duration for request paths and consumers; utilisation, saturation and errors for pools, queues and disks.
3. Choose types: counters for events, gauges for current values, histograms for durations and sizes. In Prometheus-style naming use base units such as seconds and bytes, and `_total` for counters.
4. Define labels with a known, small set of values: route template, method, status class, outcome. No user ids, emails, request ids, raw URLs or error text. Estimate series as the product of label values times instances and histogram buckets.
5. Set histogram buckets around the real latency range and the objective thresholds so they fall on boundaries.
6. Instrument at one boundary, such as middleware, and record on every exit path, including exceptions, timeouts and cancellations. Define whether client errors count as failures.
7. For queues add depth, age of the oldest item and processing outcome. For pools add in use, limit and wait time.
8. Initialise known label combinations where useful so a first failure is visible.
9. Exercise success and failure locally, inspect the metrics output, and write queries for error ratio and latency percentiles. For classic histograms, sum bucket rates by `le` before `histogram_quantile`.
10. Keep the metrics endpoint off public access and document each metric.

## Watch out for
- Averaging percentiles across instances, which is not meaningful.
- Multi-process servers reporting only one worker's values.
- Gauges that stay stale after the object disappears.
- Renaming a metric that existing alerts use.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Triggered test requests change the expected series, labels are bounded, and sample queries return sensible traffic, error and latency values.
