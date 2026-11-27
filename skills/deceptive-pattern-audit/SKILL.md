---
name: deceptive-pattern-audit
version: 1.0.0
description: >
  Audit signup, consent, checkout and cancellation flows for manipulative design and propose honest replacements. Use when reviewing a funnel for dark patterns or before changing pricing or consent screens.
author: Remedy Official
license: Apache-2.0
tags:
  - design
  - ux
  - audit
kind: native
status: discovered
tools:
  - read
  - grep
  - computer.navigate
  - computer.snapshot
  - computer.screenshot
metadata:
  source: library
  library_id: deceptive-pattern-audit
  official: true
  domain: design
  security_flags: []
---

# Deceptive Pattern Audit

## When to use
A team wants to check that its flows respect users' choices, or complaints mention surprise charges or being unable to cancel.

## Steps
1. Walk each flow as a new user on phone and desktop with test data. Stop before any real purchase or submission and ask the user.
2. Capture every screen, default, pre-checked box and the click count to accept versus decline.
3. Check money: total price and recurring terms visible before commitment, fees not appearing late, trial end and renewal stated, nothing added to the basket unasked.
4. Check choice symmetry: decline as visible and easy as accept, no shaming wording, no repeated nagging after refusal.
5. Check pressure: countdowns, stock and viewer counts. Trace each to its data source in code; flag any that reset or are fabricated.
6. Check exits: cancel, delete account and unsubscribe findable in settings, doable in the same channel as signup, without a maze of retention screens.
7. Check clarity: double negatives in toggles, ads styled as content, misleading button hierarchy.
8. Report each finding with screenshot, what a user would reasonably believe, what actually happens, severity and a concrete replacement.
9. Flag findings that may touch consumer protection or privacy law for review by a qualified lawyer, without declaring legality yourself.

## Watch out for
- Judging only the happy path misses behaviour after declining or abandoning.
- Variants from experiments or other regions may differ from what you see; check flags in code.
- Recommending removal without a replacement tends to get the report shelved.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All in-scope flows have captured evidence, each finding has a proposed honest alternative, and items needing legal review are listed separately.
