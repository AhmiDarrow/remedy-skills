---
name: cohort-retention-analysis
version: 1.0.0
description: >
  Build cohort retention tables with explicit activity definitions, complete observation windows and correct denominators. Use when asked about retention, churn curves or whether newer users stick better.
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
  library_id: cohort-retention-analysis
  official: true
  domain: data
  security_flags: []
---

# Cohort Retention Analysis

## When to use
You need to see how groups who started at different times keep returning or paying.

## Steps
1. Define the cohort entry event (signup, first purchase, activation) and use the first occurrence over full history, not the first inside the query window.
2. Define "active" as an action showing real value. Say whether background events, logins or refunds count.
3. Choose the retention type: active in period N, active in N or later (unbounded), or active in every period through N. Label it.
4. Choose calendar periods or rolling windows from each user's start; day 7 means different things in each.
5. Fix the time zone and the identity rule for users with several ids.
6. Build the table: cohort size, then distinct users meeting the rule at each age. Keep the original cohort size as denominator.
7. Generate every cohort and age combination first so true zeros appear, and mark cells whose window has not fully elapsed as empty.
8. When averaging across cohorts, weight by size and include only cohorts that reached that age.
9. Show counts beside percentages and flag small cohorts.
10. Spot-check several users end to end, and compare period 0 with the known signup count.

## Watch out for
- The newest cohort's partial period looks like a collapse.
- Blended retention can move because the acquisition mix changed while no segment changed.
- Filtering to users who are currently subscribed or not deleted makes old cohorts look far better.
- Logging changes appear as vertical or diagonal bands; check release dates before explaining them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The definitions are written above the table, incomplete cells are blank rather than zero, and hand-traced users match.
