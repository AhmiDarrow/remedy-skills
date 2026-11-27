---
name: error-state-design
version: 1.0.1
description: >
  Design what a product shows and does when something fails: causes, placement, wording, preserved input, retry and recovery paths. Use when failures show vague messages, lose work or leave users stuck.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ux
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
metadata:
  source: library
  library_id: error-state-design
  official: true
  domain: design
  security_flags: []
---

# Error State Design

## When to use
A flow needs defined failure behaviour across validation, network, server and permission problems.

## Steps
1. Trace the flow's requests and actions in code and list every way each can fail: invalid input, offline, timeout, rate limit, conflict, expired session, no permission, not found, server fault, partial success.
2. For each, record what the user can do about it, whether their input survives, and whether the action may have happened anyway.
3. Choose placement by scope: beside the field, within the affected section, a persistent banner, or a full page only when nothing else is usable. Keep working parts working.
4. Write what happened, what it affects and the next step, in the user's terms. State the cause only if the system knows it, and say what was saved.
5. Offer the matching recovery: correct, retry, reload the latest version and compare, sign in and return, request access, export a draft, contact support.
6. Preserve entered data through validation errors, retries, re-authentication and reloads where safe.
7. Make retries safe. For a timeout on payment, send or create, check status or use an idempotency key before repeating. Back off automatic retries and stop after a limit.
8. Make it perceivable: text plus icon, field errors linked to inputs, focus moved to an error summary after failed submit, status changes announced. Do not rely on a vanishing toast.
9. Show a short reference ID that matches server logs, and keep stack traces and internal details out.
10. Describe how to trigger each state in testing.

## Watch out for
- "Something went wrong" for cases the code can tell apart.
- Messages that reveal whether an account or private resource exists.
- A retry button for a failure that will always fail again.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each failure case has placement, wording, data handling and recovery defined, unsafe retries are addressed, accessibility behaviour is stated, and each state has a way to reproduce it.
