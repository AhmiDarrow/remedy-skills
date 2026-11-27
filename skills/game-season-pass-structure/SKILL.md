---
name: game-season-pass-structure
version: 1.0.1
description: >
  Structure a season pass track with fair free and paid rewards, reachable XP pacing, catch-up, clear terms and economy checks. Use when designing or reviewing a battle pass or seasonal reward track.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - liveops
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: game-season-pass-structure
  official: true
  domain: gaming
  security_flags: []
---

# Game Season Pass Structure

## When to use
A game wants a seasonal reward track that players will consider fair.

## Steps
1. State season theme, length, audience, price intent, content capacity and whether play is competitive.
2. Lay out tiers with free and paid rewards. The free track should be worth playing. Prefer cosmetics; no pay-to-win power, especially in competitive modes.
3. Show paid buyers what they get, including every reward, before purchase. Avoid padding with filler.
4. Measure XP per hour by mode and playstyle. Compute total hours and weekly hours needed for casual, regular and heavy profiles, with and without challenges.
5. Pace so the intended player finishes with slack for missed weeks. Let missed weekly challenges accumulate, add catch-up late in the season and define XP after the final tier.
6. Check challenges do not reward harmful play, such as quitting matches or ignoring team goals.
7. Model premium currency, boosts, tier skips and any currency returned by the pass, for inflation and for pressure to buy.
8. Specify buying late (earned tiers unlock), season end, unclaimed rewards, expiry, whether items return, refunds and cross-platform ownership.
9. Draft plain player-facing terms with dates and time zone.
10. List items for legal and platform review: minors, spending controls, random rewards, virtual currency, cancellation and any auto-renewal. Rules differ by region.

## Watch out for
- Pace that only works with daily play or bought boosts.
- Countdown pressure and "never again" claims that are not true.
- Changing XP rates or rewards mid-season against people who already paid.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A reward table and reproducible hours-per-profile calculation exist, edge cases and terms are written, and review items are flagged unanswered or confirmed.
