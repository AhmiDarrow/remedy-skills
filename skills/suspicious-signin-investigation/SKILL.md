---
name: suspicious-signin-investigation
version: 1.0.0
description: >
  Investigate an unexpected sign-in or access alert on an account or server you manage, deciding if it is genuine and what to revoke. Use when logs show unfamiliar locations, devices or login bursts.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - incident
  - identity
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - owner.notify
metadata:
  source: library
  library_id: suspicious-signin-investigation
  official: true
  domain: security
  security_flags: []
---

# Suspicious Signin Investigation

## When to use
An identity provider, server or application reports access nobody recognises.

## Steps
1. Open logs through the service's own console or the host, not links in the alert message, which may be phishing.
2. Gather time (in UTC), account, source address, device or client, authentication method, MFA result and success or failure.
3. Distinguish failed guessing from success. Many accounts with few attempts each suggests password spraying; many attempts on one suggests brute force or a stale stored password.
4. Rule out ordinary causes with evidence: VPN or mobile carrier egress, a new device, a sync client or automation. Ask the account owner through a channel you already trust.
5. On Linux, check `journalctl` for sshd or the auth log, and `last`; on Windows, security events 4624 and 4625 with logon type.
6. For any unexplained success, review what followed: MFA methods added, recovery details, mail forwarding and inbox rules, app consents, API tokens, new users, role changes and downloads.
7. With approval, contain: revoke all sessions and tokens, remove unknown methods and grants, then have the user set a new unique password from a clean device.
8. Search other accounts for the same sources and patterns.
9. Record verdict and evidence, and strengthen: phishing-resistant MFA, disabling legacy protocols, conditional access.

## Watch out for
- Geolocation is approximate and impossible-travel alerts are often VPN artefacts, but that must be checked, not assumed.
- Changing the password alone may leave sessions, tokens and app grants alive.
- Repeated unexpected MFA prompts mean the password is probably known.
- Disabling the only admin account can lock out the responders.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each flagged event is classed as legitimate, blocked attempt or compromise with evidence, and for compromise all persistence checks and revocations are recorded.
