---
name: strangler-migration-plan
version: 1.0.0
description: >
  Replace a legacy system piece by piece behind a routing layer, keeping it in service throughout. Use when someone proposes rewriting a working system and a big-bang switch is too risky.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - architecture
  - migration
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - write
metadata:
  source: library
  library_id: strangler-migration-plan
  official: true
  domain: backend
  security_flags: []
---

# Strangler Migration Plan

## When to use
The old system must keep serving users while its replacement is built over months.
## Steps
1. Inventory capabilities from the running system: routes, jobs, reports, integrations, admin chores. Include usage evidence where logs exist.
2. Find or add one interception point (proxy route, facade module, message dispatcher) through which calls pass, first forwarding everything to the old code with no behaviour change.
3. Choose the first slice: real but low-risk, with few data entanglements. It proves routing, deployment and rollback.
4. Decide data ownership per slice. Exactly one side is the writer of each record at any time; describe how the other side reads or receives copies.
5. Before cutover, compare outputs: replay or shadow read-only traffic and diff results. Never shadow operations that send, charge or delete.
6. Cut over behind a switch that can route back, and state what happens to data written by the new side if you do.
7. Delete the old path for each finished slice before starting too many new ones.
8. Track remaining capabilities as a shrinking list with a definition of when the old system is switched off.
## Watch out for
- Both systems writing the same tables with different rules.
- Stopping at 80 percent, which leaves two systems to maintain forever.
- Adding new features during the move so parity keeps receding; set a rule for where new work goes.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The plan names the interception point, slice order, per-slice data owner, comparison method, rollback and the condition for decommissioning.
