---
name: alert-noise-reduction
version: 1.0.0
description: >
  Cut alert fatigue by measuring which alerts led to action, then deleting, regrouping or rewriting them around user impact. Use when on-call is paged often for things that need nothing done.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - observability
  - alerting
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: alert-noise-reduction
  official: true
  domain: ops
  security_flags: []
---

# Alert Noise Reduction

## When to use
Pages are frequent, ignored or auto-resolving, and real problems hide among them.

## Steps
1. Export several weeks of alert history: name, count, time of day, duration, acknowledgement and what the responder did.
2. Rank by pages and by interruptions outside working hours. A few rules usually dominate.
3. Label each top rule: actionable and urgent; actionable but can wait; never acted on; duplicate of another.
4. For each page, require an affected user or imminent failure, an action a human must take now, and a runbook link. Otherwise make it a ticket, dashboard panel or nothing.
5. Replace cause alerts such as high CPU with symptom alerts on error rate, latency or availability, keeping predictive ones like disk or certificate running out.
6. For service objectives, use burn-rate alerts over a long and a short window together, so brief blips do not page but fast burns do.
7. Fix flapping with a hold duration, hysteresis or better aggregation, not just a higher threshold.
8. Group and inhibit in the alert router so one outage sends one notification.
9. Replay new expressions against past incidents to check each would still have fired. Review page counts again after two weeks.

## Watch out for
- A permanent silence is an invisible deletion. Give silences expiry dates.
- Removing the only alert on a failure mode needs a named replacement or an accepted risk.
- A rule over a metric that stops being reported goes quiet; alert on missing data for critical sources.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each reviewed rule is kept, rewritten or removed with a reason, past real incidents would still page, and a date is set to compare page volume.
