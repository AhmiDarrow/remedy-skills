---
name: mtu-blackhole-debug
version: 1.0.0
description: >
  Find and fix path MTU black holes where small requests work but large transfers hang over VPNs, tunnels or PPPoE links. Use when connections establish and then stall on bigger data.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - networking
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: mtu-blackhole-debug
  official: true
  domain: ops
  security_flags: []
---

# Mtu Blackhole Debug

## When to use
SSH logs in but a long listing freezes, TLS handshakes hang, or some sites load partly, often through a tunnel.

## Steps
1. Confirm the pattern: ping and TCP connect work, large payloads stall.
2. List MTUs along the parts you control with `ip link`, `netsh interface ipv4 show subinterfaces` or `ifconfig`.
3. Probe with fragmentation forbidden. Linux: `ping -M do -s 1472 <host>`. Windows: `ping -f -l 1472 <host>`. macOS: `ping -D -s 1472 <host>`.
4. Search downward for the largest payload that succeeds. For IPv4, path MTU is that payload plus 28 bytes; for IPv6 plus 48.
5. Check ping to this host works at a small size, so ICMP filtering is not misread as an MTU limit. `tracepath` can show where the value drops.
6. Compare with tunnel overhead; every encapsulation layer reduces the usable size.
7. Test a temporary lower MTU on one client's tunnel interface and repeat the failing transfer.
8. Fix at the right place: correct the tunnel MTU; allow ICMP "fragmentation needed" (IPv4) and "packet too big" (IPv6) through firewalls; or clamp TCP MSS on the router, for example nftables `tcp option maxseg size set rt mtu` on forwarded SYN packets.
9. Persist the setting in the interface or VPN config and retest after reboot.

## Watch out for
- MSS clamping helps TCP only; UDP-based protocols still need a correct MTU.
- IPv6 requires at least 1280, so setting lower breaks it.
- Blocking all ICMP is a common cause of this fault.
- Lowering every interface to a tiny value hides the problem and costs throughput.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The measured path limit is recorded, the previously hanging transfer completes in both directions, and the fix survives a restart.
