---
name: install-script-inspection
version: 1.0.0
description: >
  Inspect a downloaded install script or pipe-to-shell command before running it, tracing what it fetches, changes and persists. Use before running any curl or PowerShell one-liner installer.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - supply-chain
  - shell
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - web.fetch
metadata:
  source: library
  library_id: install-script-inspection
  official: true
  domain: security
  security_flags: []
---

# Install Script Inspection

## When to use
Documentation or a message says to paste a command that downloads and runs code.

## Steps
1. Do not run the one-liner. Confirm the URL belongs to the real project through a source independent of the page that gave you the command.
2. With the user's approval for the download, save the script into a new empty folder without piping it to an interpreter. Record URL, time and SHA-256.
3. Read it all. Decode embedded encoded strings as text only, never by executing them.
4. Trace every further download: URL, transport, version pinning and checksum or signature verification. Fetch and inspect nested scripts the same way.
5. List effects: files written, privilege elevation, users, services, scheduled tasks, shell profile edits, PATH changes, added package repositories and signing keys, firewall or security tool changes, telemetry.
6. Look for red flags: disabling protections, clearing history or logs, hidden window or silent flags, reading SSH keys, browser data or tokens, sending host details out.
7. Check failure behaviour, such as unquoted variables in deletion commands or continuing after errors.
8. Compare with a safer route: distribution or OS package, signed release asset with verification, or a container.
9. Report findings. If the owner proceeds, run the exact saved file, ideally in a disposable VM first.

## Watch out for
- A server can send different content to a terminal client than to a browser, or change it between requests; downloading again to run it defeats the review.
- Reading only the top of a long script misses the part that matters.
- A dry-run flag is only trustworthy if you read how the script implements it.
- Syntax-checking or "test running" untrusted code can still execute it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The owner has a list of downloads and system changes with concerns marked, and any execution used the hashed reviewed copy.
