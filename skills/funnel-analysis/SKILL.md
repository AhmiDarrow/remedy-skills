---
name: funnel-analysis
version: 1.0.0
description: >
  Measure step-by-step conversion with a defined unit, ordering, time window and instrumentation checks. Use when asked where users drop off in signup, checkout or onboarding.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - analysis
  - product
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: funnel-analysis
  official: true
  domain: data
  security_flags: []
---

# Funnel Analysis

## When to use
A multi-step flow needs conversion figures that can be trusted enough to prioritize fixes.

## Steps
1. List the steps with the exact event or record proving each, and where in code it fires (`grep` it). Note client-side versus server-side.
2. Choose the unit: user, session or attempt (cart, application). Count each once per funnel.
3. Define ordering (strict sequence or any order after entry) and the window from entry to completion.
4. Enter units by their first step inside the period, and only include those whose window has closed.
5. Compute each step conditional on the previous one in time order, rather than dividing independent daily event counts.
6. Report counts, step conversion, overall conversion and median time between steps.
7. Validate instrumentation against a source of truth, such as completed orders in the database versus completion events. Check duplicates and steps with more users than the one before.
8. Segment by a few dimensions known at entry (platform, source, app version).
9. Investigate the largest losses with error logs, validation failures and timing before proposing causes.
10. Size the opportunity as users lost at the step, noting that recovering them will not carry through at the average downstream rate.

## Watch out for
- Optional steps and alternate paths (express checkout, social sign-in) look like drop-off unless modelled.
- Ad blockers and lost page-unload events undercount client events.
- Anonymous-to-logged-in identity changes split one journey into two.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Definitions are written, completions reconcile with the system of record within an explained gap, and the biggest drops are shown with counts.
