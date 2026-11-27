---
name: pii-data-handling
version: 1.0.1
description: >
  Design or review how one feature handles personal data: minimising fields, limiting access, protecting copies, retention, export and deletion. Use when code starts collecting or moving personal data.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - privacy
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
  library_id: pii-data-handling
  official: true
  security_flags: []
---

# Pii Data Handling

## When to use
A change adds or exposes names, contacts, location, identifiers or other data about people. This is engineering guidance, not legal advice; lawful basis, notices and regulated categories need a qualified privacy professional.

## Steps
1. List each new or touched field, whose it is, why it is needed and which behaviour fails without it. Drop fields with no answer, or collect a coarser value (age band instead of birth date).
2. Classify them. Escalate health, biometric, financial, government ID, precise location and children's data before building.
3. Draw where each value goes: database, caches, search, queues, analytics, third parties, email, exports, backups, developer machines.
4. Limit reads: explicit response fields rather than whole records, masked display by default, role-limited access, and an audit entry for staff viewing or bulk export.
5. Protect it: TLS in transit and storage encryption at rest; add field-level encryption where database readers should not see values, and settle who holds keys and how search still works. Keep personal data out of URLs and error reports.
6. Set retention per store with a trigger and period agreed by the owner, and implement the job that enforces it.
7. Confirm the existing export and account deletion paths include the new fields and copies, including third parties; state how restored backups avoid reviving deleted records.
8. Use synthetic data in tests and non-production. Add tests that the API omits restricted fields and that the retention job removes expired rows.

## Watch out for
- Pseudonymous IDs and hashed emails can usually still be linked to a person.
- Free-text boxes collect sensitive data you never asked for.
- Generic object serialisation exposes a new column the moment it is added.
- Inspect schemas and synthetic records; do not print real people's data while reviewing.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each field has a purpose, access rule, destinations and retention, the controls are tested or listed as gaps, and legal questions are recorded for the right person.
