---
name: compromised-host-triage
version: 1.0.0
description: >
  First-response triage for a computer or server you manage that may be compromised, preserving evidence before containment and cleanup. Use when there are unknown processes, logins, miners or tampered files.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - incident
  - forensics
kind: native
status: discovered
tools:
  - bash
  - read
  - owner.notify
  - write
metadata:
  source: library
  library_id: compromised-host-triage
  official: true
  domain: security
  security_flags: []
---

# Compromised Host Triage

## When to use
You suspect an intrusion on a machine you are authorised to administer.

## Steps
1. Tell the owner and ask whether legal, insurance or regulatory handling applies; if so, stop and involve incident responders. Work from a separate trusted device for notes and credential changes.
2. Contain at the network layer (isolate the switch port, security group or VM network) while keeping the machine powered, since shutting down loses memory evidence. If data is actively being destroyed, containment urgency comes first.
3. If possible, take a VM snapshot including memory, or a disk image.
4. Record volatile state with timestamps: processes with parents and command lines, network connections, logged-in users and recent logins. On Linux, `/proc/<pid>/exe` and `cwd` identify what is really running; on Windows capture process paths and signatures.
5. Check persistence: services, timers and cron, scheduled tasks, run keys, startup folders, launch items, shell profiles, SSH authorised keys, new accounts, drivers and extensions.
6. Collect auth, system and application logs to another system and hash what you save.
7. Build a timeline and scope: entry route, first activity, other hosts and credentials reachable from here.
8. Rotate exposed credentials and revoke sessions from a clean device.
9. Rebuild from trusted media and restore data from backups predating the intrusion, then patch the entry route before reconnecting.

## Watch out for
- System tools on a compromised host can lie; compare with outside logs.
- Deleting the visible malware commonly leaves another foothold.
- Logging in with a domain or cloud admin account hands the attacker those credentials.
- Do not connect to, probe or retaliate against the attacker's systems.
- Absence of evidence in short or editable logs does not prove nothing was taken.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Evidence is preserved and listed, the host is isolated or rebuilt, exposed credentials are rotated, and scope and unknowns are reported.
