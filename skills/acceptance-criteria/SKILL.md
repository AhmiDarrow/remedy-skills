---
name: acceptance-criteria
version: 1.0.1
description: >
  Write testable acceptance criteria for a feature or bug fix, covering examples, edge cases, roles, failures and limits. Use when a ticket is vague or before implementation starts.
author: Remedy Official
license: Apache-2.0
tags:
  - product
  - testing
kind: native
status: discovered
tools:
  - read
  - write
  - grep
metadata:
  source: library
  library_id: acceptance-criteria
  official: true
  security_flags: []
---

# Acceptance Criteria

## When to use
Someone needs an agreed, checkable definition of what the change must do.

## Steps
1. Read the request and the current behaviour in code, screens or docs. Restate the user and the outcome in one sentence.
2. List open decisions and ask about those that change behaviour. Mark the rest as labelled assumptions; do not invent business rules or limits.
3. Write each criterion as one observable result: starting state, action, expected outcome. Use real example values ("a 10 MB file is accepted, 10 MB plus one byte is rejected with a size message").
4. Walk the edges that apply: empty, first and maximum; invalid input; each role and a non-owner; duplicate submission and concurrency; dependency failure; existing data created before the change.
5. State what must not happen, such as no charge, no email or no data change after a failed request.
6. For quality needs give a number, condition and way to measure it, agreed by the requester. Include keyboard and screen reader behaviour for UI.
7. For a bug, include the reproduction, the correct result and nearby behaviour that must stay unchanged.
8. Number the list, add out-of-scope items, and note how each is verified: automated test, manual check or metric.

## Watch out for
- "Works correctly", "fast" and "user friendly" cannot be failed, so they are not criteria.
- Prescribing the implementation, such as table names or widgets, when only behaviour matters.
- A criterion joining several outcomes with "and" cannot be partly passed.
- Only the happy path being specified.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A tester who was not in the discussion could mark every criterion pass or fail, and unresolved decisions are listed with who must answer them.
