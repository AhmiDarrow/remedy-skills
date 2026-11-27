---
name: sla-error-budget
version: 1.0.1
description: >
  Define service level indicators, objectives and an error budget policy from user journeys and measured history. Use when reliability targets are vague or teams argue about releases versus stability.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - sre
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: sla-error-budget
  official: true
  security_flags: []
---

# Sla Error Budget

## When to use
A service needs a measurable reliability target and a rule for acting on it. A contractual SLA is a separate promise with legal and commercial terms; flag those for the people who own contracts.

## Steps
1. Name the few user journeys that matter and what failure looks like for each.
2. Define each indicator as good events over valid events: successful and fast enough requests, fresh enough data, jobs completed on time. Write exact inclusion and exclusion rules, including client errors, health checks, test traffic and maintenance.
3. Choose where to measure. Load balancer or client data sees failures that application metrics miss when the process is down or requests never arrive.
4. Pull several weeks of history and show current performance, known incidents and data gaps.
5. Set the target from user need and demonstrated ability, with the compliance window (rolling 28 or 30 days is common). Keep the internal objective stricter than any external SLA.
6. Convert to a budget: 100% minus the objective. At 99.9% over 30 days that is 0.1% of valid events, or about 43 minutes if measured as time with total outage.
7. Check that dependencies and on-call response times make the target achievable.
8. Write the policy with the product and engineering owners: what happens at stated levels of budget use and when exhausted, such as prioritising reliability work or restricting risky releases, with exceptions for security and reliability fixes and who may grant them.
9. Define the queries, a dashboard showing remaining budget, burn-rate alerting and a review date.

## Watch out for
- A 100% target, which leaves no budget for any change.
- Low traffic services where one failure swings the ratio; use longer windows or event counts.
- Averages for latency; count requests under a threshold.
- Missing telemetry counting as success.
- A policy that nobody with release authority agreed to.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each objective has an exact query, window, historical result and budget, and the policy names triggers, actions and decision owners.
