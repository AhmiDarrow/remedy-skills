---
name: ab-test-sample-size
version: 1.0.0
description: >
  Plan an A/B test: primary metric, randomization unit, minimum detectable effect, sample size, duration and stopping rule. Use before launching an experiment.
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
  library_id: ab-test-sample-size
  official: true
  domain: data
  security_flags: []
---

# Ab Test Sample Size

## When to use
A controlled experiment is being set up and nobody has said how large or long it must be.

## Steps
1. Write the hypothesis, one primary metric, a few guardrail metrics, and the decision for a win, loss or inconclusive result.
2. Choose the randomization unit (usually user or account) and make assignment sticky.
3. Define who is eligible and log exposure at the point where the experiences actually diverge.
4. Get the baseline rate, or mean and variance, for that same population from recent data.
5. Agree the smallest effect worth acting on, and state whether it is absolute or relative.
6. Compute sample size with chosen alpha and power (0.05 and 0.8 are common conventions) using an installed statistics library or a simulation. For a rough two-arm check, n per arm is about 16 times variance divided by the squared absolute difference.
7. Convert to duration from eligible new units per day, not page views, and cover whole weekly cycles.
8. If the unit of analysis differs from the randomization unit (sessions while randomizing users), account for correlation with user-level aggregation, the delta method or clustered errors.
9. Fix the stopping rule: a fixed horizon, or a sequential method chosen now.
10. Run an A/A or dry run to verify assignment ratio and logging.

## Watch out for
- Halving the detectable effect needs about four times the sample.
- Using an observed effect from an underpowered pilot as the target usually overstates it.
- Extra variants and metrics need a stated multiple-comparison plan.
- If the required duration is unrealistic, say so and change the metric or question instead of running anyway.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A written plan holds metric, unit, baseline, effect size, sample, duration and stopping rule, agreed before data arrives.
