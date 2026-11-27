---
name: linux-server-hardening
version: 1.0.0
description: >
  Apply a baseline hardening pass to a Linux server you manage, driven by its exposed services and accounts, with verification and rollback. Use when preparing or auditing a server, especially an internet-facing one.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - linux
  - hardening
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - write
metadata:
  source: library
  library_id: linux-server-hardening
  official: true
  domain: security
  security_flags: []
---

# Linux Server Hardening

## When to use
A server needs a security baseline. SSH and firewall changes have their own careful procedures; follow those for the edits.

## Steps
1. State the server's role and required inbound and outbound flows. Confirm console access and a snapshot.
2. List listeners with `ss -tulpn`, enabled units, accounts with login shells, sudo rules including NOPASSWD, and every `authorized_keys`.
3. Check release support and pending security updates; enable an update routine.
4. Remove or disable services with no required purpose; bind internal ones to loopback or private addresses.
5. Verify exposure from another machine with a port scan of your own host, on IPv4 and IPv6.
6. Remove stale accounts and keys, give people individual accounts, and narrow sudo rules. Watch for rules allowing editors, interpreters or wildcards that yield a root shell.
7. Check permissions on secrets and find world-writable paths and scripts run by root that other users can modify.
8. Keep SELinux or AppArmor enforcing, and sandbox network services through their units.
9. Send auth and system logs off the host, keep time synchronised, and confirm backups.
10. Run an audit tool such as Lynis or an OpenSCAP profile as a checklist, judging each item against the role rather than chasing a score.

## Watch out for
- Pasting a bulk sysctl or benchmark script can break routing, containers or the application.
- Disabling a service without checking dependants can break monitoring or backups.
- Container-published ports and cloud security groups are separate exposure layers.
- Hardening without a record makes later faults very hard to trace.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Only documented ports are reachable, accounts and privilege rules are justified, the application passes health checks after reboot, and accepted gaps are listed.
