---
name: dns-resolution-debug
version: 1.0.0
description: >
  Debug a name that resolves wrongly or not at all by comparing local, recursive and authoritative answers. Use when a domain works for some people or machines and fails for others.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - dns
  - networking
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: dns-resolution-debug
  official: true
  domain: ops
  security_flags: []
---

# Dns Resolution Debug

## When to use
Lookups fail, return old addresses or differ between machines.

## Steps
1. Record the exact name, record type, failing client and error. NXDOMAIN, SERVFAIL, timeout and an empty answer mean different things.
2. Ask what the client really uses: `resolvectl query` on systemd-resolved Linux, `Resolve-DnsName` on Windows, `dscacheutil -q host -a name <name>` on macOS. `dig` bypasses parts of the OS resolver path, including the hosts file.
3. Check hosts file entries, VPN or split-DNS rules, search suffixes and browser DNS-over-HTTPS.
4. Query specific recursive resolvers with `dig @<resolver> <name> <type>` and compare answers and TTLs.
5. Find the authoritative servers with `dig NS <zone>` and query each with `+norecurse`. Disagreement between them points to failed zone propagation.
6. Walk delegation with `dig +trace`. Compare NS records at the parent with those in the zone.
7. On SERVFAIL, retry with `+cd`. If that succeeds, suspect DNSSEC: check DS at the parent against the zone's keys and signature expiry.
8. For NXDOMAIN after creating a record, check negative caching, bounded by the zone's SOA settings.
9. Flush only the caches that are stale, after saving the bad answer.

## Watch out for
- CNAME cannot sit beside other data at the same name, and a standard CNAME is not allowed at the zone apex.
- An AAAA record pointing nowhere breaks only IPv6-capable clients.
- Split-horizon DNS makes inside and outside answers legitimately differ.
- Lowering a TTL now does not shorten copies already cached with the old one.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The layer returning the wrong answer is identified with query output, and the failing client resolves correctly or the remaining cache expiry time is stated.
