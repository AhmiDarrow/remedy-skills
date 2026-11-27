---
name: dns-record-migration
version: 1.0.0
description: >
  Move a domain to a new DNS host or change critical records with a full export, TTL lowering, DNSSEC care and a rollback. Use before switching nameservers or repointing a live domain.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - dns
  - migration
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - todo
metadata:
  source: library
  library_id: dns-record-migration
  official: true
  domain: ops
  security_flags: []
---

# Dns Record Migration

## When to use
A zone is changing provider, or records serving websites or mail are about to move.

## Steps
1. Export the full zone from the current host. Public queries cannot list all records, so do not rebuild it from guesses.
2. Note provider-specific features that plain zone files lack: apex aliasing, redirects, proxying, geo or health-checked answers. Plan an equivalent for each.
3. Record whether DNSSEC is enabled, including DS records at the registrar.
4. Lower relevant TTLs, then wait at least as long as the old TTL.
5. Create the zone at the new host and compare record by record by querying old and new nameservers directly: A, AAAA, CNAME, MX, TXT, SRV, CAA and delegations.
6. Handle DNSSEC explicitly: either a supported multi-signer transfer, or remove the DS, wait out its TTL, move, and re-sign afterwards.
7. The user changes nameservers at the registrar.
8. Keep both zones serving identical data for at least the delegation TTL, commonly up to two days. Apply any edit to both.
9. Verify website, mail send and receive, certificate renewal and third-party domain verifications.
10. Restore normal TTLs and only then retire the old zone.

## Watch out for
- A stale DS record with new unsigned nameservers makes the whole domain fail on validating resolvers.
- Missing DKIM or verification TXT records break quietly, days later.
- Deleting the old zone early strands resolvers still holding old delegation.
- A CAA record can block the new certificate issuer.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Both public and authoritative queries match the planned records, mail and HTTPS checks pass, and the old zone is retired only after the overlap period.
