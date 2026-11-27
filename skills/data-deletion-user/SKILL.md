---
name: data-deletion-user
version: 1.0.1
description: >
  Build account deletion that confirms identity, cuts access at once and erases or anonymizes data across every store. Use when adding "delete my account" or handling erasure in your own product.
author: Remedy Official
license: Apache-2.0
tags:
  - privacy
  - backend
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: data-deletion-user
  official: true
  security_flags: []
---

# Data Deletion User

## When to use
Users must be able to delete their account and the data tied to it.

## Steps
1. Inventory where the user's data lives: tables and foreign keys, uploads, search index, caches, queues, analytics, logs, third-party processors and backups.
2. Decide per item: delete, anonymize or retain. Retention needs a named reason and period (invoices, fraud records); have a qualified person confirm legal obligations rather than guessing.
3. Settle shared data: documents in a team, messages others received, an organisation whose sole owner is leaving, active subscriptions and balances.
4. Require fresh re-authentication and a clear summary of what will be lost. Offer export first where it exists.
5. Immediately mark the account pending deletion, revoke sessions, API keys and linked-app tokens, stop emails and recurring billing. With a grace period, say how to cancel it.
6. Run erasure as a resumable job with per-store status. Each step must be safe to repeat; a failed step retries and alerts, and the job is not complete until all succeed.
7. Request deletion from processors through their supported method and record the response.
8. Define backup expiry, and keep a minimal deletion ledger so a restore re-applies deletions.
9. Test on synthetic accounts: seed every store, delete, then search each for the user's ids, email and files. Confirm others' data survived.

## Watch out for
- A `deleted_at` flag alone is hiding, not erasure.
- Cascades can remove other people's shared records.
- Anonymizing the name while email or IP stays in free text or logs.
- The audit entry itself must not copy the deleted personal data.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A test account is deleted end to end, a search of every inventoried store finds only documented retained records, and old sessions and keys are rejected.
