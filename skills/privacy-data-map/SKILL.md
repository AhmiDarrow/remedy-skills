---
name: privacy-data-map
version: 1.0.0
description: >
  Build an inventory of personal data a product or organisation holds, where it flows, why, who gets it and how long it stays. Use before a privacy review, policy draft or handling access and deletion requests.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - privacy
  - compliance
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - write
metadata:
  source: library
  library_id: privacy-data-map
  official: true
  domain: security
  security_flags: []
---

# Privacy Data Map

## When to use
Nobody can say with evidence what personal data a system collects. This supports, and does not replace, legal advice.

## Steps
1. Set scope: products, environments and business processes.
2. Search code for evidence: database schemas and migrations, API request models, forms, analytics calls, logging statements, file uploads, third-party SDKs and outbound hosts.
3. Add what code does not show: spreadsheets, support inboxes, vendor dashboards, backups, exports, test copies and paper.
4. For each category record data subjects, fields, source, purpose, system and location, access roles, recipients, region, retention and deletion method.
5. Mark special or high-risk categories such as health, biometrics, precise location, children's data, government IDs and financial details.
6. Include derived and inferred data, device identifiers, IP addresses and free-text fields that collect anything.
7. Trace one real flow end to end using synthetic test data to confirm the map.
8. Flag mismatches: collected without a purpose, kept indefinitely, sent to an undisclosed recipient, or contradicting the published notice.
9. List questions of lawful basis, contracts, transfers and notices for a qualified privacy professional.
10. Store the map beside the code with an owner and update it when schemas or vendors change.

## Watch out for
- Copying real records into the inventory creates a new sensitive dataset; list field names only.
- Hashed or tokenised identifiers are usually still linkable to a person.
- Retention written in policy may not be what the system does; check actual deletion jobs and backup expiry.
- SDKs can collect more than your own code sends.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every personal data category found has purpose, location, recipients and retention or an explicit unknown, with evidence references and an owner for each gap.
