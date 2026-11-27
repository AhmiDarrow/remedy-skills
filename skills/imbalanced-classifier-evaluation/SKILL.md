---
name: imbalanced-classifier-evaluation
version: 1.0.0
description: >
  Evaluate and threshold a classifier for rare events using precision-recall, calibration and error costs instead of accuracy. Use when positives are scarce, as in fraud, failure or churn prediction.
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
  - bash
  - write
metadata:
  source: library
  library_id: imbalanced-classifier-evaluation
  official: true
  domain: data
  security_flags: []
---

# Imbalanced Classifier Evaluation

## When to use
One class is rare and a headline accuracy or ROC figure hides whether the model is useful.

## Steps
1. State positive prevalence in the real deployment population and in each split.
2. Describe the action taken on a positive, its capacity (reviews per day) and the relative cost of misses and false alarms.
3. Keep validation and test sets at natural prevalence. Resample or reweight only training folds.
4. Report the precision-recall curve and average precision, with prevalence as the no-skill precision. ROC AUC can look high while most alerts are false.
5. Pick the operating threshold on validation data from costs, capacity or a required recall or precision. Do not default to 0.5.
6. At that threshold, show the confusion matrix in counts per realistic period, and precision at k if work is ranked.
7. If probabilities drive decisions, check a reliability curve. Class weighting and resampling distort probabilities, so recalibrate on natural-prevalence data.
8. Give intervals by bootstrapping; with few positives they are wide.
9. Break results down by important segments and by time.
10. Freeze the threshold, evaluate once on test, and set a plan to revisit it when prevalence changes.

## Watch out for
- Synthetic oversampling before splitting puts near-copies in both sets.
- If only flagged cases are ever investigated, new labels are biased toward what the old model found; keep a small reviewed random sample if the process allows.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The threshold has a written reason, expected true and false alerts per period are stated, and test data kept natural prevalence.
