---
name: wireguard-tunnel-setup
version: 1.0.0
description: >
  Set up a WireGuard tunnel with correct keys, AllowedIPs, routing, firewall and handshake verification. Use when connecting your own devices or sites over an encrypted link.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - vpn
  - networking
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: wireguard-tunnel-setup
  official: true
  domain: ops
  security_flags: []
---

# Wireguard Tunnel Setup

## When to use
You need private access between machines you control, or WireGuard is configured but passes no traffic.

## Steps
1. Decide topology: one device to server, hub for several, or site to site. List which subnets each side should reach.
2. Pick a tunnel subnet that does not overlap either LAN; common home ranges collide with other networks.
3. Generate a key pair on each device with `wg genkey` and `wg pubkey`, using a restrictive umask. Private keys stay on their device and out of chat.
4. Write each interface: its address and private key; for each peer a public key and AllowedIPs. Set a listen port and endpoint where reachable.
5. Understand AllowedIPs: it is both the outbound route selector and the filter on accepted source addresses. On a hub, give each client its own /32; do not overlap peers. Use `0.0.0.0/0` (and `::/0`) only for full tunnelling.
6. Add `PersistentKeepalive = 25` on a peer behind NAT that must stay reachable.
7. Open only the UDP port. For LAN access through the server, enable IP forwarding and add either return routes on the LAN or NAT.
8. Bring it up and run `wg show`. Check latest handshake and byte counters, then ping the tunnel address, then a LAN host, then DNS.
9. Enable at boot and record how to revoke a lost device by removing its peer.

## Watch out for
- No handshake points to endpoint, port, firewall, NAT or wrong public keys; a handshake without traffic points to AllowedIPs or routing.
- WireGuard stays quiet to unauthenticated packets, so port scans prove little.
- A full-tunnel client with unchanged DNS can leak lookups or lose name resolution.
- Enabling it remotely with a wide route can cut your own session.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Handshakes are recent, only intended subnets are reachable, the tunnel returns after reboot, and a removed peer can no longer connect.
