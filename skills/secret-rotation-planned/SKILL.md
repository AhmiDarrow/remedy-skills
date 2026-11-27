---
name: secret-rotation-planned
version: 1.0.0
description: >
  Rotate passwords, API keys or signing keys without downtime using overlap, a full consumer inventory and proof the old value is dead. Use when a credential is due, a person leaves or ownership changes.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - secrets
  - ops
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - todo
  - owner.notify
metadata:
  source: library
  library_id: secret-rotation-planned
  official: true
  domain: security
  security_flags: []
---

# Secret Rotation Planned

## When to use
A credential must change on a planned basis. A known leak needs immediate containment first.

## Steps
1. Identify the secret by name and ID, never printing its value. Find all consumers: services, CI, cron jobs, scripts, developer machines, third parties and backups of config.
2. Cross-check code search with the provider's last-used and access logs to catch unlisted consumers.
3. Determine whether two values can be valid at once. If not, use two alternating accounts or schedule a short window.
4. For signing or encryption keys, plan separately: verifiers must trust the new public key before anything signs with it, old signatures need the old key until they expire, and old encrypted data needs decryption or re-encryption.
5. Create the new credential with equal or narrower permissions. The user handles values that must be typed.
6. Put it in the secret store, not in files in the repository or command arguments.
7. Roll consumers one by one, reloading or restarting as each requires, and verify a real authenticated action.
8. Watch usage of the old credential until it stops, covering the longest job interval.
9. Disable it, observe, then delete after approval.
10. Update the inventory and next rotation trigger.

## Watch out for
- Updating the store does nothing for processes holding the value in memory.
- Existing database connections and issued tokens can outlive the old password.
- Changing a session signing key without overlap logs everyone out.
- Encrypting data with a key and then deleting the old key makes earlier data unrecoverable.
- Shell history and CI debug output are common new leak points during rotation.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All consumers authenticate with the new credential, the old one is shown to be rejected, and the inventory is updated.
