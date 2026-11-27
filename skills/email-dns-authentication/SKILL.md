---
name: email-dns-authentication
version: 1.0.0
description: >
  Set up SPF, DKIM and DMARC for a domain you control, moving from monitoring to enforcement without losing legitimate mail. Use when mail lands in spam or others can spoof your domain.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - dns
  - email
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - web.fetch
metadata:
  source: library
  library_id: email-dns-authentication
  official: true
  domain: security
  security_flags: []
---

# Email Dns Authentication

## When to use
A domain needs sender authentication, or an existing setup is failing.

## Steps
1. Inventory every system that sends as the domain: mailbox host, billing, support desk, website forms, newsletters, servers.
2. Query current TXT records for the domain, known DKIM selectors at `<selector>._domainkey`, and `_dmarc`.
3. Publish exactly one SPF record listing the real senders, using each vendor's current documented include. Stay within the limit of 10 DNS-lookup mechanisms, counting nested includes.
4. Enable DKIM signing in each sending service with its own selector, publish the keys, and use 2048-bit RSA where supported.
5. Publish DMARC with `p=none` and a `rua` address that someone will process. Reports to another domain need that domain's authorising record.
6. Send test messages from every source to a mailbox you own and read the Authentication-Results header.
7. Check alignment: DMARC passes only if SPF or DKIM passes with a domain aligned to the visible From address.
8. Review aggregate reports for several weeks, fixing legitimate sources.
9. With the owner's approval, move to `quarantine` and then `reject`, watching reports at each stage. Check subdomain policy too.
10. For domains that send no mail, publish `v=spf1 -all` and a reject DMARC policy.

## Watch out for
- Two SPF records produce a permanent error, not a merge.
- Forwarding commonly breaks SPF, so aligned DKIM matters.
- Jumping straight to reject can silently drop invoices and password resets.
- Passing authentication does not guarantee inbox placement.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every known sender shows an aligned DMARC pass in real headers, and the published policy matches the agreed stage.
