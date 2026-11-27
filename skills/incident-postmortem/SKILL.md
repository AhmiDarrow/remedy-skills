---
name: incident-postmortem
version: 1.0.1
description: >
  Write a blameless incident postmortem with an evidenced timeline, contributing causes and owned, verifiable actions. Use after an outage, data problem or near miss has been stabilised.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - docs
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: incident-postmortem
  official: true
  security_flags: []
---

# Incident Postmortem

## When to use
An incident is over and the team needs to learn from it.

## Steps
1. Gather sources before they expire: chat and incident log, alerts, deploy and config history, graphs, logs and tickets. Use the team's template if one exists.
2. Build a UTC timeline with a source for each entry. Include when the fault was introduced, impact began, detection, response, mitigation and verified recovery. Mark gaps and estimates.
3. Quantify impact: who, which functions, duration, failed or delayed operations, data affected and error budget used. State how figures were obtained.
4. Calculate time to detect and time to mitigate from the timeline.
5. Explain the mechanism from trigger to user impact. Test that each link is supported by evidence, and label hypotheses.
6. List contributing conditions: why the change passed review and tests, why the safeguard did not stop it, why detection or recovery took as long. Do not stop at "human error"; ask what made the action reasonable at the time with what the person could see.
7. Record what worked and where luck limited damage.
8. Write a few actions that change prevention, detection, mitigation or blast radius. Each has one owner, priority, due date, tracker link if present and a way to verify it. Distinguish completed from proposed.
9. Write a summary that a reader outside the team understands, then ask participants to correct the facts before it is shared.

## Watch out for
- Naming individuals as causes; use roles where identity adds nothing.
- Hindsight wording such as "obviously" or "should have noticed".
- "Be more careful" or "add training" standing in for a system fix.
- Customer data, tokens or security detail in a widely shared document.
- Inventing owners or dates; mark them unassigned.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The timeline and impact are sourced, causes explain both occurrence and detection, actions are verifiable with owners or flagged unassigned, and open questions are listed.
