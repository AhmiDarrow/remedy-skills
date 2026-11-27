---
name: multi-step-form-wizard
version: 1.0.0
description: >
  Design and build a multi-step form with sensible step grouping, per-step validation, safe back navigation and resume. Use when a long signup, application or checkout flow is being split.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - forms
  - ux
kind: native
status: discovered
tools:
  - read
  - edit
  - computer.navigate
  - computer.snapshot
metadata:
  source: library
  library_id: multi-step-form-wizard
  official: true
  domain: frontend
  security_flags: []
---

# Multi Step Form Wizard

## When to use
A single long form loses people, or an existing wizard forgets answers and validates at the wrong time.

## Steps
1. List every field with why it is needed and when it can first be known. Drop or defer the unjustified ones before designing steps.
2. Group by topic as the user thinks of it. Put questions that can disqualify or change later steps early.
3. Define the branching as data: each step's id, fields, validation schema and condition for appearing. Compute progress from the steps that currently apply.
4. Keep one answer object above the steps. Moving back or switching branches must not erase input; exclude hidden branch values only at submission.
5. Validate the current step on Next. Check cross-step rules where the later field is entered, and re-validate everything on the server at the end.
6. Give each step a URL or history entry so the browser Back button moves one step, and redirect deep links whose prerequisites are missing.
7. On step change, move focus to the new heading and announce position such as step 2 of 4.
8. Persist drafts according to sensitivity. Never store passwords or payment data in browser storage.
9. Add a review step with edit links that return straight to review afterwards.
10. Make final submission idempotent and block double sends while keeping a retry path.

## Watch out for
- A server error for a step-one field shown only on the last screen strands the user; map each error back to its step and link there.
- A progress bar that moves backwards when a branch appears reads as a punishment; show named steps if the count varies.
- Pressing Enter should trigger Next, not skip to final submit.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Forward, back, refresh, deep link, branch switch and a server-side rejection have each been exercised and none loses valid input or submits twice.
