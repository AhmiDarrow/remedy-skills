---
name: firewall-change-safely
version: 1.0.0
description: >
  Change firewall rules on a remote host with a backup, syntax check and automatic revert so you cannot lock yourself out. Use before editing nftables, iptables, ufw or Windows Firewall over the network.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - networking
  - firewall
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
metadata:
  source: library
  library_id: firewall-change-safely
  official: true
  domain: security
  security_flags: []
---

# Firewall Change Safely

## When to use
Rules must change on a machine you reach through the very network path being filtered.

## Steps
1. Confirm out-of-band access (console, hypervisor or provider rescue). If there is none, say so before continuing.
2. Identify which tool actually owns the rules: firewalld, ufw, raw nftables or iptables, a container engine, or Windows Defender Firewall. Use that one layer.
3. Save current effective rules, for example `nft list ruleset`, `iptables-save` or `netsh advfirewall export`.
4. List listening services and current client addresses so required traffic is explicit, including IPv6.
5. Write new rules that first allow established connections, loopback, necessary ICMP and your management access, then specific services, then default deny.
6. Syntax-check where possible (`nft -c -f <file>`).
7. Schedule an automatic revert a few minutes ahead with `at` or `systemd-run` (on Windows, a one-time scheduled task running as SYSTEM that re-imports the export), and confirm it is scheduled. Test the restore file loads. Saved nft output needs a preceding `flush ruleset` to replace instead of append.
8. Apply, then open a brand-new management session; the old one proves nothing.
9. Test allowed and denied ports from another host.
10. Cancel the revert only after both succeed, then persist the rules and verify after a planned reboot.

## Watch out for
- Setting a drop policy before adding the allow rules cuts the session mid-script.
- `nft flush ruleset` also removes rules created by container engines and other tools.
- Dropping ICMPv6 breaks IPv6 neighbour discovery.
- Runtime-only changes vanish at reboot, and persisted untested ones appear then.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A new management session works, outside tests match the intended allow list for IPv4 and IPv6, rules persist, and the pending revert is cancelled.
