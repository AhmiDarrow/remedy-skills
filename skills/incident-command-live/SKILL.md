---
name: incident-command-live
version: 1.0.0
description: >
  Coordinate a live outage with severity, assigned roles, a running log, one-change-at-a-time mitigation and a steady update cadence. Use when production is broken right now.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - incident
  - coordination
kind: native
status: discovered
tools:
  - todo
  - read
  - bash
  - write
  - owner.notify
metadata:
  source: library
  library_id: incident-command-live
  official: true
  domain: ops
  security_flags: []
---

# Incident Command Live

## When to use
An incident is in progress. Writing the retrospective afterwards is a separate task.

## Steps
1. State impact in one sentence: who cannot do what, since when, how many. Pick severity from the team's definitions, rounding up while unsure.
2. Establish who decides, who operates and who communicates. In a solo setup, say that the owner decides and you investigate and record.
3. Open a timestamped log in UTC. Record observations, hypotheses, actions and results, marking which is which.
4. Ask what changed: deploys, flags, config, certificates, traffic, scheduled jobs and provider status.
5. Mitigate before diagnosing fully: roll back, disable a feature, shed load, fail over. Present each option's risk and get approval.
6. Make one production change at a time with a stated expected effect and a time to check it.
7. Save volatile evidence before restarts: logs, thread or heap dumps, queue depths.
8. Send updates on a fixed interval even with nothing new: impact, current action, next update time. Draft them; the owner sends.
9. Declare mitigated only on user-facing signals, then watch a stability window before resolved.
10. List follow-ups: temporary changes to undo, data to repair, silences to remove.

## Watch out for
- Several people changing things at once makes cause and effect unreadable.
- A hypothesis repeated often starts to sound confirmed. Keep asking what evidence would disprove it.
- Failover or mass restart can cause a second outage from cold caches and reconnect storms.
- Long incidents need explicit handoffs of current state.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Impact is verified over, the log is complete, and every temporary measure has an owner and a removal condition.
