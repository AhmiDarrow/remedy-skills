---
name: browser-login-handoff
version: 1.0.0
description: >
  Pause a browser task cleanly for sign-in, two-factor, CAPTCHA or payment, then resume safely. Use when automation reaches a step only the user may complete.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - browser
  - safety
kind: native
status: discovered
tools:
  - computer.navigate
  - computer.snapshot
  - computer.screenshot
  - owner.notify
metadata:
  source: library
  library_id: browser-login-handoff
  official: true
  domain: tooling
  security_flags: []
---

# Browser Login Handoff

## When to use
A task in the browser is blocked by authentication, a human check or a sensitive entry.

## Steps
1. Stop before touching the sensitive field.
2. Verify the page's domain and note how you arrived. A sign-in prompt reached from an email or ad link deserves a warning; suggest opening the site from a bookmark.
3. Tell the user in one message what is needed, where, why, and what you will do afterwards.
4. Use `owner.notify` if they are away, without including codes, account numbers or private page content.
5. Wait. Do not try alternative logins, reset flows, saved passwords or another account.
6. When they say they are done, take a fresh snapshot instead of trusting the earlier state.
7. Confirm which account is signed in and that it is the intended one, especially with work and personal profiles.
8. Check where you landed; sites often return to the home page and discard form progress.
9. Resume from the last verified step. Re-check anything that may have changed.

## Watch out for
- Never ask the user to paste a password or one-time code into chat.
- Never solve, outsource or work around a CAPTCHA or bot check.
- An unexpected two-factor prompt that nobody initiated should be denied and reported.
- Screenshots during credential entry can capture secrets; do not take them.
- "Remember this device" and permission grants are the user's choices.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The user completed the protected step themselves, the right account is confirmed from a new snapshot, and the task resumed or is clearly parked.
