---
name: permissions-matrix
version: 1.0.1
description: >
  Build a role-by-action permission matrix and check it against what the server actually enforces, with tests for the denials. Use when defining roles, auditing access control or answering who can do what.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - product
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: permissions-matrix
  official: true
  security_flags: []
---

# Permissions Matrix

## When to use
Access rules are scattered through code or exist only in people's heads.

## Steps
1. List actors, including anonymous, each role, resource owner, other tenant's user, service accounts and support staff.
2. Inventory actions from routes, resolvers, jobs and admin tools rather than from the menus. Name them as verb and resource.
3. For each cell record allow, deny or conditional, with the condition spelled out: own record, same team, record state, plan. Default is deny.
4. Mark each cell's source: product decision, or merely observed in code. Send undecided cells to a named owner instead of inferring intent.
5. Trace each action to its server-side check and note file and line. Compare, and record: missing check, check looser or stricter than intended, or enforced only in the UI.
6. Look at side doors: export, bulk and search endpoints, field-level updates, invitation and role changes (can someone grant more than they hold, or remove the last owner), and stale access after role removal.
7. Generate table-driven tests from the matrix covering critical allows and denials, asserting both the response and that nothing changed.
8. Add a check that fails when a new route has no declared permission, where the framework allows it.
9. Publish a plain version for support and admins.

## Watch out for
- A role check without an ownership or tenant check lets any member act on any record.
- A matrix kept only in a document drifts; tie it to tests or policy code.
- Permissions cached in tokens survive revocation until expiry.
- Report suspected holes before changing behaviour that users may rely on.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every inventoried action has a decision or a named open question, each critical denial has a passing test, and mismatches are listed with locations.
