---
name: game-build-checklist
version: 1.0.1
description: >
  Verify a game release candidate on the exact shippable package: version, stripped cheats, saves, clean install, performance and known issues. Use before submitting or publishing a build.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - release
kind: native
status: discovered
tools:
  - read
  - write
  - grep
  - glob
  - bash
  - todo
metadata:
  source: library
  library_id: game-build-checklist
  official: true
  domain: gaming
  security_flags: []
---

# Game Build Checklist

## When to use
A build is about to go to players, a store or platform certification.

## Steps
1. Pin the candidate: commit, version and build number, platform, configuration and artifact checksum. It must show the number in game. Any rebuild is a new candidate.
2. Build from a clean checkout with the release configuration; read warnings and cook or asset logs for missing or fallback content.
3. Inspect the package: no debug menus, cheats, test accounts, development server addresses, secrets, editor-only or unlicensed assets. Check symbols are kept privately and match this build.
4. Install on a clean machine or account without development tools. Test first boot, shortest path to gameplay, offline behaviour, quit and relaunch.
5. Load saves from every released version, and test interrupted writes, full storage and missing permissions.
6. Run the platform basics: suspend and resume, controller disconnect, focus loss, resolutions, language switch, and entitlement or add-on checks.
7. Play the critical path or run its tests, plus a soak run; compare load time, memory and frame time with the budget on the weakest supported device.
8. Trigger a test crash and confirm it arrives symbolicated, respecting the player's consent setting.
9. Check current certification or store requirements from the platform's own documentation, plus credits, notices, ratings and store assets.
10. Publish a table: pass, fail, not run, with evidence; known issues with severity and who accepted each. Submit only on the user's go-ahead.

## Watch out for
- Testing the editor or development build and approving the release one.
- "Quick fix, no retest" after sign-off.
- No rollback plan, or a new save format that an older build cannot read after rollback.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every check on the exact artifact is pass, fail or not run with a reason, and blockers and the ship decision owner are named.
