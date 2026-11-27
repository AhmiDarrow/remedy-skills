---
name: ml-data-leakage-audit
version: 1.0.0
description: >
  Audit a model pipeline for target, temporal, group and preprocessing leakage before trusting its score. Use when validation results look too good or production performance falls far below them.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - ml
  - evaluation
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: ml-data-leakage-audit
  official: true
  domain: data
  security_flags: []
---

# Ml Data Leakage Audit

## When to use
A trained model's offline score is about to be trusted, or has already failed to hold up.

## Steps
1. Write the prediction moment: what exactly is known when the model is called in production.
2. For every feature, trace its source and ask whether that value existed at that moment. Watch for fields updated after the outcome, such as status, closing reason or lifetime totals.
3. Check point-in-time joins: each lookup must use rows valid before the prediction time.
4. Check the label window, and that features do not overlap it.
5. Match the split to deployment: time-based for forecasting the future; grouped when several rows share a user, patient, device or document.
6. Search for duplicates and near-duplicates across splits.
7. `grep` for fitting done before splitting: scaling, imputation, vocabulary, target encoding, feature selection, resampling. Move each inside the training fold.
8. Check test data was not used for tuning, early stopping or repeated model choice.
9. Probe: inspect top feature importances, score a model on each suspicious feature alone, and see whether ids or row order predict the label. Training on shuffled labels should give chance-level results through the whole pipeline.
10. Remove the leaks, re-evaluate on an untouched later period, and report old and new scores.

## Watch out for
- File names, collection site or image dimensions can encode the class.
- A lower score after the fix is the honest result, not a regression to tune away.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each feature is shown to be available at prediction time, the split mirrors deployment, and the re-evaluated score is reported.
