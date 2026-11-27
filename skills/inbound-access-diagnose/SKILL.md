---
name: inbound-access-diagnose
version: 1.0.0
description: >
  Work out why a port forward or home-hosted service is unreachable from outside, covering CGNAT, double NAT, firewalls and IPv6. Use when something works on the LAN but not from the internet.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - networking
  - selfhost
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: inbound-access-diagnose
  official: true
  domain: ops
  security_flags: []
---

# Inbound Access Diagnose

## When to use
Inbound connections to a network you control fail.

## Steps
1. Confirm the service answers from another LAN device on the host's LAN address, and note whether it listens on loopback only.
2. Allow it in the host firewall and give the host a stable DHCP reservation.
3. Compare the router's WAN address with the public address seen from outside. If they differ, there is another NAT upstream. A WAN address in 100.64.0.0/10 indicates carrier-grade NAT; a private range indicates a second router or the provider's modem.
4. Behind a second router you own, use bridge mode or forward on both. Behind carrier NAT, port forwarding cannot work: choose a public IPv4 from the provider, IPv6, a VPN through a server you control, or a tunnel service.
5. Check the forward rule's protocol, external port, internal address and internal port.
6. Test from a truly external network, such as a phone on mobile data, while capturing on the host to see whether packets arrive.
7. Consider provider blocking of particular ports.
8. For IPv6, publish the host's stable address and add an inbound allow rule; no port forward is involved.
9. Before leaving it open, confirm the service is patched and authenticated. Prefer VPN access for admin panels.

## Watch out for
- Testing the public address from inside fails on routers without NAT loopback even though outsiders can connect.
- A changing public address needs dynamic DNS.
- Automatic UPnP mappings can open ports nobody reviewed.
- Opening a "DMZ host" exposes every port on that machine.
- Never expose remote desktop or database ports directly as a quick test.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
An external client reaches only the intended service, or the blocking hop is identified and a workable alternative is chosen with its exposure explained.
