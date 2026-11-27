---
name: missing-data-handling
version: 1.0.0
description: >
  Diagnose why values are missing and choose deletion, imputation or flags without biasing results or leaking information. Use when a dataset has gaps that affect analysis or a model.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - statistics
  - cleaning
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: missing-data-handling
  official: true
  domain: data
  security_flags: []
---

# Missing Data Handling

## When to use
Nulls or blanks are common enough that how you treat them could change the answer.

## Steps
1. Find disguised missing values: empty strings, "N/A", 0, -1, 9999, 1970-01-01.
2. Tabulate missingness by column, over time, by source and by group, and see which columns go missing together.
3. Trace the mechanism in forms and pipeline code: not applicable, not asked, refused, lost in a join, collected only after a date.
4. Compare outcomes and key variables between rows with and without the value.
5. Classify plausibly: unrelated to anything, explainable by observed variables, or dependent on the unseen value itself. Data alone cannot prove which.
6. Fix upstream bugs first when values are recoverable.
7. Choose by purpose: keep "not applicable" as its own category; use complete cases only with a reason; for inference consider multiple imputation so uncertainty is carried; for prediction, impute and add a missing indicator, or use a model that handles nulls natively.
8. Fit imputers on training data only, inside each cross-validation fold.
9. Run a sensitivity analysis with at least one pessimistic assumption and see whether the conclusion holds.
10. Report the missing share per variable and the method.

## Watch out for
- Filling with the mean shrinks variance and weakens relationships.
- Forward-filling a time series invents observations and may use values from after the prediction time during backfills.
- SQL aggregates skip NULLs, so `AVG(x)` and `SUM(x) / COUNT(*)` differ.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each affected variable has a stated mechanism hypothesis and treatment, and the headline result is shown to be stable or flagged as sensitive.
