---
name: model-drift-monitoring
version: 1.0.0
description: >
  Monitor a deployed model for input drift, prediction shifts and delayed-label performance, with clear responses. Use when a model goes to production or its quality quietly degrades.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - ml
  - monitoring
kind: native
status: discovered
tools:
  - read
  - write
  - bash
  - routines.create
  - owner.notify
metadata:
  source: library
  library_id: model-drift-monitoring
  official: true
  domain: data
  security_flags: []
---

# Model Drift Monitoring

## When to use
A model serves real decisions and the world it was trained on can change.

## Steps
1. Log per prediction: id, time, model and feature versions, score, decision and the features or a permitted summary. Agree retention and access for sensitive data.
2. Note how and when true outcomes arrive, and join them back by prediction id.
3. Check pipeline health first: schema, null rate, unseen categories, out-of-range values, stale features, fallback rate.
4. Compare serving features with training features for the same entities to catch training-serving skew.
5. Track input and score distributions against a fixed reference, matched for season, using a distance or stability measure. Set limits from historical variation.
6. Prioritize important features; with large volumes, statistical tests flag trivial differences.
7. When labels arrive, compute the real metric by prediction-date cohort, only for mature cohorts, plus calibration and key segments.
8. While labels lag, use named proxies such as override or complaint rate.
9. Account for feedback: decisions can prevent the outcome being observed.
10. For each alert define the first check, owner and options: fix data, adjust threshold, retrain, roll back or use a rule fallback. Compare any retrained model on the same recent holdout before replacing.

## Watch out for
- Input drift does not prove performance fell, and stable inputs do not prove it held.
- Automatic retraining on corrupted data ships the corruption.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
An injected feature fault raises an alert, mature cohorts report real performance, and rollback has been tried.
