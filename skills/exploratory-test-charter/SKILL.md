---
name: exploratory-test-charter
version: 1.0.0
description: >
  Run time-boxed exploratory testing guided by a charter, taking notes that turn findings into bugs and tests. Use when a new feature needs probing beyond the scripted tests.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - exploratory
  - qa
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - computer.snapshot
  - computer.click
  - computer.type
metadata:
  source: library
  library_id: exploratory-test-charter
  official: true
  domain: testing
  security_flags: []
---

# Exploratory Test Charter

## When to use
Automated checks pass, and nobody has yet tried to use the thing carelessly or creatively.
## Steps
1. Write a charter: explore a named area, with named techniques or data, to find a named kind of risk. Set a time box of about an hour.
2. Use a test environment and synthetic accounts. Confirm the build version before starting.
3. Vary one dimension at a time across tours: interruptions (close, sleep, lose network mid-save), repetition (double submit, undo and redo many times), data extremes (very long, empty, right-to-left, emoji), navigation (back, deep link, two windows), environment (small window, keyboard only, wrong system date in a disposable VM only).
4. Observe beyond the screen: logs, console errors, files written, resource use.
5. Keep running notes with time, action, observation and questions.
6. When something looks wrong, reproduce it once and capture steps and evidence before moving on.
7. Follow surprising behaviour; it often clusters.
8. Debrief: bugs, open questions, areas covered, areas not reached and the next charter. Propose automated tests for findings worth guarding.
## Watch out for
- Wandering without notes, so findings cannot be repeated.
- Testing against real user data or sending real messages or payments.
- Reporting "no bugs" without saying what was never touched.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The time box is complete with a debrief listing reproducible findings, coverage and untested areas.
