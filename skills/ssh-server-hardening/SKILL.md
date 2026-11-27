---
name: ssh-server-hardening
version: 1.0.0
description: >
  Harden an SSH server without losing access by testing keys first, checking effective settings and keeping a recovery session. Use when a server accepts password or root SSH logins.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - linux
  - ssh
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: ssh-server-hardening
  official: true
  domain: security
  security_flags: []
---

# Ssh Server Hardening

## When to use
An SSH service you administer needs tighter authentication or exposure.

## Steps
1. Confirm console or rescue access and keep one working session open throughout.
2. Inventory who and what logs in, including backup jobs and automation, from auth logs and `authorized_keys` files.
3. Have each user create a key on their own device with a passphrase, install only the public key, and prove key login in a new session.
4. Read effective settings with `sshd -T`. Check `/etc/ssh/sshd_config.d/`: for most directives the first value read wins, so an early drop-in can override your later edit.
5. Set `PasswordAuthentication no`, `KbdInteractiveAuthentication no` unless it serves MFA through PAM, and `PermitRootLogin no` (or `prohibit-password` if automation truly needs root).
6. Restrict with `AllowGroups`, making sure your own account is in the group first. Limit automation keys with options such as `from=`, `restrict` and a forced command.
7. Disable forwarding features that are not used.
8. Validate with `sshd -t`, reload, and open a new connection. Also verify password login is refused.
9. Limit source networks in the firewall or put SSH behind a VPN; rate-limit or ban repeated failures.

## Watch out for
- On socket-activated distributions, changing `Port` in sshd_config may not move the listener; check the ssh socket unit.
- `Match` blocks can silently re-enable settings; test with `sshd -T -C user=<name>,host=<host>,addr=<ip>`.
- A nonstandard port reduces log noise but is not a control.
- Old keys of departed users stay valid until removed.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
New key logins work for every required user and job, password and disallowed root attempts fail, and `sshd -T` shows the intended values.
