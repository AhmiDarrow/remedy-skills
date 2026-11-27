---
name: ml-error-analysis
version: 1.0.0
description: >
  Improve a model by sampling and categorising its mistakes, separating label, data and model faults before changing anything. Use when a metric has plateaued or a model fails on certain cases.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - ml
  - debugging
kind: native
status: discovered
tools:
  - read
  - bash
  - write
  - todo
metadata:
  source: library
  library_id: ml-error-analysis
  official: true
  domain: data
  security_flags: []
---

# Ml Error Analysis

## When to use
You have a working model and need to decide what would improve it most.

## Steps
1. Fix a development set for analysis and keep the final test set unseen.
2. Save each prediction with input reference, label, score, model version and useful slice attributes.
3. Compare against a trivial baseline and the training score to see whether the gap is fitting or generalizing.
4. Sample errors: random false positives and false negatives, plus the most confident wrong ones, which often expose label faults.
5. Read at least several dozen by hand and assign categories that emerge from them: wrong label, ambiguous, missing information, broken preprocessing, rare subgroup, shortcut feature, genuine model miss.
6. Count categories and estimate how much the metric could gain if each were fixed.
7. Compute metrics by slice with sample counts, and compare error rates, not just error counts.
8. For suspected preprocessing faults, inspect the exact tensor, tokens or feature vector the model receives.
9. Choose one intervention tied to the largest fixable category, state the expected effect, and rerun.
10. Diff predictions old versus new: newly fixed and newly broken.

## Watch out for
- Correcting labels only where the model disagrees biases the data toward the model; use the same relabelling rule on a sample of agreements.
- Repeatedly tuning to the same development errors overfits it; refresh it periodically.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A counted error breakdown justifies the chosen change, and the before-and-after diff shows what it fixed and broke.
