---
name: job-quote-estimate
version: 1.0.0
description: >
  Build an itemised quote for a small-business job with materials, labour, overhead, margin and stated assumptions. Use when pricing custom work so it does not lose money.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - small-business
  - pricing
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: job-quote-estimate
  official: true
  domain: data
  security_flags: []
---

# Job Quote Estimate

## When to use
A tradesperson, freelancer or shop needs to price a specific job.

## Steps
1. Write the scope from the request and site notes; list unknowns that could change price.
2. Break the work into tasks including travel, setup, cleanup, admin and callbacks.
3. List materials with quantity, current supplier price and date, plus the user's waste allowance.
4. Price labour at a loaded cost covering wages or target pay, payroll costs and non-billable time.
5. Add subcontractors, equipment, permits and an overhead share from the user's figures.
6. Apply profit and keep markup and margin distinct: margin = (price - cost) / price. A 25% markup is only a 20% margin.
7. Treat uncertainty with a stated allowance, range or provisional item.
8. Compare with similar past jobs, estimated versus actual.
9. Produce the customer copy with scope, exclusions, validity, deposit and change process, keeping internal costs out.

## Watch out for
- Guessing tax rates or whether tax applies; the user or their accountant confirms.
- Calling it a fixed quote when it is an estimate.
- Old material prices.
- Formulas that omit a newly added row.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Totals recompute correctly, every cost input has a source, and the customer copy states assumptions and expiry.
