---
name: onboarding-ui-flow
version: 1.0.1
description: >
  Design first-run onboarding around a measurable activation moment, covering steps, setup checklist, skip and resume, permission timing and instrumentation. Use when new users stall or drop out early.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ux
  - product
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: onboarding-ui-flow
  official: true
  domain: design
  security_flags: []
---

# Onboarding Ui Flow

## When to use
A product needs a first-run flow, a getting-started checklist, or a fix for either.

## Steps
1. Define activation as an observable action that shows the user got value, not "finished the tour". Use data to support it if available; otherwise call it a hypothesis.
2. `read` the current signup and first-run code and list every field, screen, permission and wait before activation. Remove, default, infer or defer each that is not required.
3. Map entry paths: new account, invited teammate, returning half-done user, imported data, second device. They should not all get the same steps.
4. Teach in context: let people do the real task with defaults, templates or clearly labelled sample data. Avoid long carousels and tooltip chains.
5. Request each permission when the feature needs it, after saying why, with a working path if declined.
6. If a setup checklist helps, use about three to five real tasks ordered by value. Each links to where it is done and is ticked from actual product state, so work done elsewhere counts.
7. Make it skippable and dismissible, with an obvious way back. Hide it after completion and do not show it as new work to established users.
8. Persist progress per user (and per workspace for shared setup) on the server where it must follow devices, with a version so later changes behave predictably.
9. Design empty, failed and waiting states, plus keyboard and screen reader use of any overlay.
10. Define events for start, each step, skip, dismiss and activation, without content or personal data, and compare activation and later retention, not only completion.

## Watch out for
- Counting skips as completion, or pre-ticking tasks the user never did.
- Overlays that block the very control they point at.
- Invitations or imports that send messages without the user confirming recipients.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The flow specifies activation, each entry path and step with skip, resume, persistence, permission and failure behaviour, plus events to measure it, with assumptions labelled.
