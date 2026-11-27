---
name: home-network-segmentation
version: 1.0.0
description: >
  Split a home or small office network into VLANs or separate segments for trusted devices, guests, smart devices and servers. Use when untrusted gadgets share a network with important machines.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - homelab
  - networking
kind: native
status: discovered
tools:
  - read
  - write
  - web.fetch
  - todo
metadata:
  source: library
  library_id: home-network-segmentation
  official: true
  domain: security
  security_flags: []
---

# Home Network Segmentation

## When to use
Cameras, televisions and guest phones can currently reach computers and storage.

## Steps
1. Inventory devices from the router's lease table and physical checks, with what each must talk to.
2. Confirm hardware support: router or firewall with inter-VLAN rules, a managed switch, and access points that map SSIDs to VLANs. If missing, use the router's guest network and say what it does not cover.
3. Keep the segments few, for example trusted, servers, smart devices, guest, and management.
4. Give each a VLAN ID and subnet, avoiding ranges that collide with VPNs you use.
5. Plan ports: access ports carry one untagged VLAN; trunks to access points and switches carry the tagged set.
6. Write the traffic matrix with default deny between segments. Trusted may start connections to smart devices; the reverse is blocked apart from named needs. All segments get only the DNS, DHCP and time services they require.
7. Block untrusted segments from the router's own admin interface and from private subnets, in IPv6 as well.
8. Back up current configs. Build and test one segment while keeping a wired management port on the old network.
9. Move devices in groups and test casting, printing and hub discovery.

## Watch out for
- mDNS discovery does not cross subnets without a reflector, which should be limited to needed VLANs.
- Removing the management VLAN from your own uplink locks you out.
- A server with interfaces in two segments becomes a bridge around the rules.
- Many consumer devices only join 2.4 GHz networks.
- A guest label does not prove isolation; test it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
From each segment, allowed destinations work and a forbidden one, including the router admin page, is shown unreachable.
