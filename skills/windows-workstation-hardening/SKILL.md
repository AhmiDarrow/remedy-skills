---
name: windows-workstation-hardening
version: 1.0.0
description: >
  Audit and tighten a Windows PC or small fleet covering updates, accounts, Defender, firewall, remote access and encryption. Use when securing a personal or small office Windows machine.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - windows
  - hardening
kind: native
status: discovered
tools:
  - bash
  - read
  - owner.notify
metadata:
  source: library
  library_id: windows-workstation-hardening
  official: true
  domain: security
  security_flags: []
---

# Windows Workstation Hardening

## When to use
A Windows computer you administer needs a practical security pass. Query first; change only with approval.

## Steps
1. Record edition, version, support status and whether it is managed by organisation policy, which may override local changes.
2. Check updates for Windows, browsers, office software, runtimes and firmware. Flag software with no updates.
3. Review `Get-LocalGroupMember Administrators`. Daily work should use a standard account, with a separate admin credential and UAC left on.
4. Read `Get-MpComputerStatus` and `Get-MpPreference`: real-time and cloud protection, tamper protection, signature age and exclusions. Investigate unexplained exclusions, especially whole drives, temp folders or script hosts.
5. Consider attack surface reduction rules in audit mode first, review events, then enforce. Evaluate controlled folder access the same way.
6. Check all firewall profiles are on, then list enabled inbound allow rules and `Get-NetTCPConnection -State Listen` with owning processes.
7. Disable unused remote access and legacy protocols such as SMB1; remove remote tools nobody recognises after confirming what they are. Never leave RDP exposed to the internet.
8. Review startup items, services and scheduled tasks for unsigned programs in user-writable paths.
9. Verify drive encryption and recovery key custody, screen lock and a restorable backup.
10. Re-test needed apps, printing and remote support, and record each change with how to reverse it.

## Watch out for
- "Debloat" and one-click hardening scripts disable updates or security services.
- Removing the last working admin account locks you out.
- A second antivirus changes Defender's mode, so verify which product is actually protecting.
- An unknown remote access tool may indicate a scam or intrusion; investigate before deleting evidence.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A before-and-after report covers each area, protections show enabled, required workflows work and remaining risks have an owner.
