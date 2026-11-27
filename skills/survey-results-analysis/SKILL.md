---
name: survey-results-analysis
version: 1.0.0
description: >
  Analyse survey responses with data cleaning, response-bias checks, correct bases, uncertainty and careful reading of scales and comments. Use when given survey exports to summarise or compare.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - analysis
  - surveys
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: survey-results-analysis
  official: true
  domain: data
  security_flags: []
---

# Survey Results Analysis

## When to use
Raw survey results need to become findings people can act on.

## Steps
1. Get the questionnaire as respondents saw it, with routing logic, invitation list, send dates and incentives.
2. Count invited, started and completed. Compare respondents with the invited population on known attributes.
3. Clean with rules written before looking at results: duplicates, test entries, impossibly fast completion, failed attention checks. Report removals.
4. Separate not shown, skipped, "don't know" and zero. State the base (n) for every figure.
5. For multi-select questions, report share of respondents and note totals exceed 100%.
6. For rating scales, show the full distribution. Use top-box or median summaries as extras, and confirm direction of reverse-coded items.
7. Show uncertainty. For small groups, give counts and avoid decimals. A margin of error assumes random sampling and does not cover self-selection.
8. Weight only if reliable population totals exist; report weighted and unweighted and watch for large weights.
9. Code open comments into themes with a written definition, count them, and keep uncommon but severe issues visible.
10. Anonymize quotes and suppress small segments where a person could be identified.

## Watch out for
- Comparing waves with changed wording, order or audience measures the change in method.
- Leading or double-barrelled questions cannot be repaired in analysis; flag them.
- Percentages among people routed to a follow-up are not percentages of all respondents.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every figure has its base, the response bias and cleaning are described, and conclusions are limited to who actually answered.
