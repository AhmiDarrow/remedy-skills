---
name: audit-log-design
version: 1.0.1
description: >
  Design an audit trail for sensitive user and admin actions with an event schema, reliable writes, tamper protection and retention. Use when a system must answer who did what, to which record, and when.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - ops
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - write
metadata:
  source: library
  library_id: audit-log-design
  official: true
  security_flags: []
---

# Audit Log Design

## When to use
A system needs accountable records, separate from debugging logs.

## Steps
1. List the questions the trail must answer for investigations, support and any stated compliance duty. Have the owner or an adviser confirm legal requirements.
2. Search the code with `grep` for sensitive paths: sign-in and failures, credential and two-step changes, role and permission changes, key creation, data export, bulk reads of sensitive data, deletion, impersonation, configuration and audit settings. Include jobs, scripts and direct admin tools.
3. Define a versioned schema: event ID, action name, server UTC time, actor ID and type, real actor behind impersonation or delegation, tenant, target type and ID, outcome (allowed, denied, failed), reason, source and request ID.
4. For changes, record allowlisted field names and safe before/after values. Never log passwords, tokens, keys or full request bodies. Encode user-controlled text to prevent log injection.
5. Take actor and tenant from the authenticated server context, never from client input.
6. Decide delivery per event: write in the same transaction as the change, or through a transactional outbox. State whether the action is refused if auditing fails, and alert on write failures.
7. Make storage append-only for the application identity. For stronger needs, ship copies to a separately administered store with retention locks or hash chaining, and monitor gaps.
8. Set retention and deletion per event class, including personal data duties.
9. Restrict reading by tenant and role, record access and exports of the trail, then test allowed, denied, failed and rolled-back cases.

## Watch out for
- Logging only successes, which hides probing.
- Fire-and-forget writes that vanish in a crash.
- A hash chain kept where the same administrator can rewrite everything proves little.
- IP addresses taken from forwarded headers without a trusted proxy.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each listed sensitive action maps to an event with defined delivery, protection, retention and access, and tests or named gaps show coverage.
