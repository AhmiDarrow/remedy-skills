---
name: cloud-leaked-key-response
version: 1.0.0
description: >
  Contain a leaked cloud or API credential by revoking it, hunting for what it did and removing anything the attacker left behind. Use when a key shows up in a repository, log, paste or alert.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - cloud
  - incident
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - owner.notify
  - todo
metadata:
  source: library
  library_id: cloud-leaked-key-response
  official: true
  domain: security
  security_flags: []
---

# Cloud Leaked Key Response

## When to use
A secret may have been seen by someone who should not have it. Assume it was used.

## Steps
1. Tell the owner now. Identify the credential by ID or last four characters, never by pasting its value.
2. Determine what it can access and when it was first exposed.
3. With approval, disable it immediately; do not wait for the history cleanup. If production depends on it, issue a replacement and switch over in the shortest possible window.
4. Revoke sessions and temporary tokens derived from it. Deactivating a key may not end sessions already issued; follow the provider's revocation procedure.
5. Preserve audit logs, then search them from first exposure for the key and every identity it created or assumed: unfamiliar source addresses, enumeration, denied calls.
6. Hunt for persistence: new users, keys, roles, trust changes, identity providers, functions, scheduled rules, instances in all regions, shared snapshots and disabled logging.
7. Contain confirmed attacker resources, snapshotting what is needed for evidence before deletion.
8. Remove the secret from the source, and from Git history if useful, only after rotation.
9. Record the timeline and add prevention: push scanning, short-lived credentials, narrower scope. Flag possible data access so the owner can get legal or privacy advice on notification duties.

## Watch out for
- Rewriting history does not unleak anything: forks, clones and caches keep copies.
- Deleting the key at once can remove convenient last-used details; disable first.
- Checking only your usual region misses mining workloads elsewhere.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The old credential is proven rejected, attacker activity is either listed and removed or shown absent in the named log range, and gaps in logging are stated.
