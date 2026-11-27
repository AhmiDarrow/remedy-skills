---
name: deploy-canary-rollout
version: 1.0.0
description: >
  Plan and run a canary release with written traffic steps, comparison metrics, bake times and automatic abort rules. Use before shipping a risky change to a service with live traffic.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - deploy
  - observability
kind: native
status: discovered
tools:
  - read
  - bash
  - todo
  - owner.notify
metadata:
  source: library
  library_id: deploy-canary-rollout
  official: true
  domain: ops
  security_flags: []
---

# Deploy Canary Rollout

## When to use
A change could hurt users and the platform can send part of the traffic or fleet to the new version.

## Steps
1. Name what could go wrong with this particular change and which signal would show it first.
2. Confirm old and new versions can run side by side: database schema, cache formats, queue messages and API contracts must work in both directions for the whole rollout.
3. Choose steps, for example 1, 10, 50 and 100 percent, and a bake time for each long enough to collect enough requests and cover slow effects such as memory growth or periodic jobs.
4. Compare the canary with a baseline of the old version over the same window, not with yesterday. Track error rate, tail latency, saturation, restarts and one business signal such as completed checkouts.
5. Write abort thresholds as numbers before starting, with a minimum sample size.
6. Write the exact rollback command and verify you have permission to run it.
7. Deploy the first step. Check that traffic really reaches the canary and that metrics are labelled by version.
8. At each gate record the numbers, then promote, hold or abort. Ask the owner before the step that exposes most users.

## Watch out for
- At 1 percent of low traffic, zero errors can mean almost no requests. Extend the bake or send authorised synthetic traffic.
- Aggregate dashboards dilute a fully broken canary into a tiny blip; always split by version.
- Sticky sessions or long-lived connections keep traffic from moving the way the percentage suggests.
- Workers and cron jobs are not governed by load balancer weights and need their own gate.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The rollout reached 100 percent or was aborted according to the written thresholds, with the numbers at every gate recorded.
