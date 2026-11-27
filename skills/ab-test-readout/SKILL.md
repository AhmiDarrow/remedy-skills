---
name: ab-test-readout
version: 1.0.0
description: >
  Analyse a finished A/B test, checking assignment health before estimating effects with intervals and guardrails. Use when someone asks whether a variant won.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - experiments
  - statistics
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: ab-test-readout
  official: true
  domain: data
  security_flags: []
---

# Ab Test Readout

## When to use
Experiment data exists and a ship decision depends on it.

## Steps
1. Retrieve the original plan: primary metric, population, duration, stopping rule. If none exists, say the analysis is exploratory.
2. Test for sample ratio mismatch with a chi-square test of observed counts against the planned split. A very small p-value (teams often use below 0.001) means assignment or logging is broken; stop and debug.
3. Check for units in both arms, unequal exposure logging, mid-test ramp or targeting changes, bot traffic, and outages.
4. Analyse by assigned group from first exposure. Do not drop users based on behaviour the treatment could influence.
5. Aggregate to the randomization unit before computing variance.
6. Report each arm's value, the absolute difference, relative lift and confidence interval, not only a p-value.
7. For heavy-tailed metrics such as revenue, check the influence of the largest units; use a pre-stated cap or bootstrap.
8. Check guardrails with intervals too; "not significant" does not show no harm.
9. Treat segment findings not named in the plan as hypotheses for a new test.
10. Give the decision against the plan: ship, do not ship, or inconclusive, with the range of effects still plausible.

## Watch out for
- Repeatedly checking a fixed-horizon test and stopping at the first significant result inflates false positives.
- Early lifts can be novelty; look at effect by days since first exposure, cautiously.
- A p-value above the threshold is not evidence that the variants are equal.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Health checks are reported, the primary metric has an effect and interval, and the recommendation follows from the pre-stated rule or is labelled exploratory.
