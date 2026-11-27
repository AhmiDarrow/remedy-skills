---
name: runbook-write
version: 1.0.1
description: >
  Write an on-call runbook for a service or alert with verified commands, decision points, safe mitigations and escalation. Use when responders rely on memory or an alert has no instructions.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - ops
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: runbook-write
  official: true
  security_flags: []
---

# Runbook Write

## When to use
Someone unfamiliar with a service may have to diagnose or recover it under pressure.

## Steps
1. Choose the scope: one alert or one service. Read deploy config, scripts, alert rules, past incidents and existing notes.
2. Open with what the service does for users, owner, severity guide, where it runs, access needed and how to get it.
3. Start each scenario with the trigger as the responder sees it: alert name or user symptom, impact and urgency.
4. Give a first-five-minutes check list of read-only commands: health, recent deploys, error rate, resources and dependencies. For each show where to run it, expected healthy output, and what to do on each unexpected result.
5. Turn diagnosis into branches ("if the queue age is rising and workers are idle, go to..."), ending in a mitigation or escalation.
6. For each action state the effect, risk, preconditions, approval needed, how to verify and how to undo. Mark destructive steps clearly and place the target check right before them.
7. Cover deploy rollback and restart, including when rollback is unsafe because of data changes.
8. List dependencies, dashboards and logs by exact link or name, escalation contacts by role with when to call, and a communication template.
9. Verify commands in a safe environment or read-only against the real one with permission. Mark every untested command as unverified.
10. Link the runbook from the alert, add owner and last-tested date, and have someone else walk through it.

## Watch out for
- Secrets pasted into commands; say where to obtain them.
- Placeholders that look like real values in destructive commands.
- Instructions hosted only on the system that is down.
- "Check the logs" without saying which, for what and what follows.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A newcomer can go from alert to mitigation or escalation, commands are tested or marked unverified, and the runbook has an owner and test date.
