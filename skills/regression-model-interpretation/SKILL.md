---
name: regression-model-interpretation
version: 1.0.0
description: >
  Fit and explain a regression correctly: functional form, diagnostics, coefficient meaning and limits on causal claims. Use when asked what drives an outcome or what a coefficient means.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - statistics
  - modeling
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: regression-model-interpretation
  official: true
  domain: data
  security_flags: []
---

# Regression Model Interpretation

## When to use
A linear or logistic model is used to describe relationships, not only to predict.

## Steps
1. State whether the goal is description, prediction or a causal effect. Causal questions need a design and a stated confounding argument, not just more controls.
2. Choose the family by outcome: continuous, binary, count (Poisson or negative binomial, with exposure offset) or time to event with censoring.
3. Select variables from what happens before the outcome and why. Do not control for mediators or common effects of treatment and outcome.
4. Report rows dropped for missing values and compare them with rows kept.
5. Check form with residual plots; add transforms or splines where relationships bend.
6. Check clustering and repeated measures, and use clustered or robust errors or a mixed model as appropriate. Inspect influential points.
7. Examine collinearity when coefficients flip or have huge intervals.
8. Interpret in units: change in outcome per unit holding the other included variables fixed. With interactions, a main effect applies where the other term is zero or at its reference.
9. For logistic models, odds ratios are not risk ratios, especially for common outcomes; show predicted probabilities for realistic profiles.
10. Report intervals, sample size, events, reference categories and the specifications you tried.

## Watch out for
- Coefficients of different units cannot be ranked as importance.
- Selecting variables by p-value and then reporting those p-values overstates certainty.
- Control coefficients usually should not be read as effects at all.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Diagnostics are shown, the main results are stated in plain units with intervals, and the wording claims association unless the design supports more.
