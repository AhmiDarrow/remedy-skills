---
name: macos-app-blocked-diagnose
version: 1.0.0
description: >
  Diagnose why macOS blocks an app or denies it access, separating Gatekeeper, code signature, architecture and privacy permissions. Use when a Mac app will not open or silently cannot reach files or devices.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - macos
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: macos-app-blocked-diagnose
  official: true
  domain: security
  security_flags: []
---

# Macos App Blocked Diagnose

## When to use
An app is reported damaged or unverified, quits on launch, or cannot use the camera, microphone, screen or folders.

## Steps
1. Record the exact dialog, macOS version, chip type, and where the app was downloaded from.
2. Verify the source is the real publisher. If unsure, stop here.
3. Inspect the signature with `codesign --verify --deep --strict --verbose=2 <app>` and `codesign -dv --verbose=4 <app>`; compare the Team ID with one the publisher documents.
4. Check Gatekeeper's verdict with `spctl -a -vv <app>`, and the download flag with `xattr -l <app>`.
5. For launch crashes, read the crash report and Console messages; check the binary architecture with `file` against the machine.
6. A broken signature or "damaged" message: download again from the publisher. Do not repair it by re-signing.
7. For a trusted but unnotarized app, explain the risk and let the user approve it through Privacy & Security settings.
8. For denied access, check the matching Privacy & Security category for this app, or for the terminal or parent process launching it. Quit and reopen after the user changes it.
9. If permission state is stuck, `tccutil reset <Service> <bundle-id>` limited to that app forces a fresh prompt.

## Watch out for
- Disabling Gatekeeper or System Integrity Protection weakens the whole machine and is not a troubleshooting step.
- Pasting a quarantine-removal command from a download page is a common malware instruction.
- Moving or modifying an app can change how macOS identifies it and its permissions.
- Managed Macs may enforce policy; involve the administrator.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The blocking mechanism is named with command or log evidence, and the app works through a legitimate approval or is deliberately not run, with the reason given.
