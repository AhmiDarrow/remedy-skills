---
name: statistic-verification
version: 1.0.0
description: >
  Check what a headline number actually measures and whether it supports the sentence around it. Use when a percentage, ranking, average or growth figure matters to a decision or a draft.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - research
  - data
kind: native
status: discovered
tools:
  - web.search
  - web.fetch
  - bash
metadata:
  source: library
  library_id: statistic-verification
  official: true
  domain: docs
  security_flags: []
---

# Statistic Verification

## When to use
A number is persuasive and nobody has looked at how it was produced.

## Steps
1. Find the originating table or release and note the series name, unit, period and publication date.
2. Name the numerator and the denominator in words. "30% of users" needs to say which users: all, active, or survey respondents.
3. For changes, separate percentage points from percent. A rise from 4% to 6% is 2 points and a 50% increase.
4. Recover absolute values for any relative figure. "Risk doubled" from 1 in 100,000 reads very differently from 1 in 10.
5. Check the baseline and window. Try neighbouring start years and see whether the trend survives.
6. Check comparability: definition changes, series breaks, revisions, nominal versus inflation-adjusted, totals versus per capita.
7. For surveys, find sample size, who was asked, how they were recruited and the exact question. A self-selected poll does not generalise whatever its size.
8. Recompute the figure from the source table in `bash` or by shown arithmetic, and write a sentence that claims no more than the data does.

## Watch out for
- "Average" may be mean or median; with skewed data such as income they diverge widely.
- A ranking can flip with the metric or with one very small denominator.
- Rounded inputs may not reproduce the published total exactly. Say so rather than forcing a match.
- Preliminary figures are often revised. Record the vintage you used.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The number is reproduced from its source or marked unreproducible, and the final sentence states unit, population and period.
