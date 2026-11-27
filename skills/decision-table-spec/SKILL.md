---
name: decision-table-spec
version: 1.0.0
description: >
  Specify tangled business rules as a decision table that exposes missing and conflicting cases. Use when behaviour depends on several conditions combined and prose or nested ifs have become unclear.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - requirements
  - business-rules
kind: native
status: discovered
tools:
  - read
  - grep
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: decision-table-spec
  official: true
  domain: docs
  security_flags: []
---

# Decision Table Spec

## When to use
Rules like "free shipping for members over a threshold, except oversized items, unless a promotion applies" keep producing edge-case bugs.
## Steps
1. List the independent conditions. Reduce each to a small set of values; turn numeric ones into ranges with explicit inclusive or exclusive edges.
2. List the outcomes the rules can produce, including "reject" and "ask a person".
3. Enumerate combinations. The row count is the product of the value counts; if it explodes, split into two tables that run in sequence.
4. Fill the outcome for each row from the code, the spec or the owner. Leave unknown rows blank and visible.
5. Mark combinations that cannot occur and state what enforces that; if nothing does, define the behaviour anyway.
6. Merge rows only when a condition truly does not matter, shown as a dash, then confirm merged rows do not overlap with conflicting outcomes. If order matters, declare "first match wins".
7. Review the blank and surprising rows with the user.
8. Make the table drive a parameterised test, one case per row, plus cases on each range edge. Where it simplifies the code, implement the rules as data too.
## Watch out for
- Hidden conditions such as date, locale, currency or user role that never got a column.
- Overlapping ranges ("under 100" and "100 or less").
- A catch-all default row that quietly swallows cases nobody decided.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every reachable combination has exactly one outcome, and a test enumerates the rows and passes or lists the rows the code currently violates.
