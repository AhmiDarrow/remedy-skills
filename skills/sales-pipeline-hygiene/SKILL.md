---
name: sales-pipeline-hygiene
version: 1.0.0
description: >
  Review a sales pipeline for stale, unqualified or wishful deals and produce an honest forecast view. Use when forecasts keep missing or the CRM is full of dead opportunities.
author: Remedy Official
license: Apache-2.0
tags:
  - data
  - sales
  - forecasting
kind: native
status: discovered
tools:
  - read
  - bash
  - write
metadata:
  source: library
  library_id: sales-pipeline-hygiene
  official: true
  domain: data
  security_flags: []
---

# Sales Pipeline Hygiene

## When to use
A pipeline export needs cleaning before anyone trusts its totals.

## Steps
1. Load an export, keeping the original, with stage, amount, close date, owner, last activity and next step.
2. Write down each stage's exit evidence as buyer actions, such as agreed a next meeting or shared decision process.
3. Flag: past close dates, no dated next step, age far beyond typical for the stage, repeated date pushes, missing decision maker or amount, duplicates.
4. Compute historical conversion and cycle length from closed deals, if there are enough to mean something.
5. Compare each flagged deal with its stage evidence and propose advance, move back, update or close-lost with reason.
6. Present committed, likely and upside separately with the rule for each.
7. Show concentration: how much depends on the largest few deals.
8. Give owners the questions; change records only after approval.

## Watch out for
- Treating stage probability defaults as measured odds.
- Internal activity such as a sent email counting as buyer progress.
- Mass-closing deals with long legitimate cycles.
- Copying contact personal data into side files.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every flagged deal has a reason and proposed action, and the forecast states its rules and concentration.
