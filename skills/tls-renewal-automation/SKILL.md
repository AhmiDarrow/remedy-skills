---
name: tls-renewal-automation
version: 1.0.0
description: >
  Automate certificate issue and renewal with ACME, including the right challenge type, reload hooks, expiry monitoring and a failure drill. Use when certificates are renewed by hand or have expired.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - tls
  - automation
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
  - routines.create
  - owner.notify
metadata:
  source: library
  library_id: tls-renewal-automation
  official: true
  domain: ops
  security_flags: []
---

# Tls Renewal Automation

## When to use
Certificates need to renew reliably without someone remembering.

## Steps
1. Inventory every certificate and every place a copy is installed: web servers, proxies, load balancers, mail, VPN, appliances.
2. Check for existing ACME clients or timers so two tools do not manage one certificate.
3. Choose the challenge. HTTP-01 needs the CA to reach port 80 for that name. DNS-01 works for private hosts and is required for publicly trusted wildcards. TLS-ALPN-01 needs control of port 443.
4. For DNS-01, give the client a DNS token limited to the one zone or a delegated validation subdomain, stored readable only by its service user. The user creates and enters it.
5. Test against the CA's staging endpoint to avoid production rate limits.
6. Point servers at the client's stable live paths rather than copying files by hand.
7. Add a deploy hook that validates configuration and reloads each consumer.
8. Confirm the schedule exists, and for certbot run `certbot renew --dry-run`. A dry run may not exercise deploy hooks, so test the hook separately.
9. Monitor the certificate actually served on each endpoint and alert well before expiry, with margin for several failed attempts.
10. Write the manual recovery steps.

## Watch out for
- A renewed file with an unreloaded process still expires on the wire.
- Certificate lifetimes are getting shorter; renew by remaining lifetime or the CA's renewal information, not a fixed calendar.
- A new firewall rule or redirect can break HTTP-01 months later.
- CAA records must permit the chosen CA.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A staging or dry-run renewal succeeds, the hook reloads each consumer, and an independent check reports served expiry dates with alerting.
