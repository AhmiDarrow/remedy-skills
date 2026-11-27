---
name: progression-curve
version: 1.0.1
description: >
  Design and test XP, level and unlock curves against target play time and content supply. Use when levelling feels grindy or too fast, or when planning unlock pacing and catch-up.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - systems
kind: native
status: discovered
tools:
  - read
  - write
  - bash
metadata:
  source: library
  library_id: progression-curve
  official: true
  domain: gaming
  security_flags: []
---

# Progression Curve

## When to use
Players need a pace of growth, or an existing curve has walls, dead stretches or runs out of content.

## Steps
1. Collect targets: time to first reward, to main-content completion and to cap, session length, and sessions per week for casual and heavy players.
2. Measure or estimate XP per minute by game stage for slow, typical and fast players. Label guesses.
3. Derive requirements backward: XP to next level equals target minutes times expected XP per minute at that level. Fit a formula or a table afterward; keep the table if designers need local control.
4. Tabulate per level: XP step, cumulative XP, minutes, cumulative hours, unlock. Put it in CSV so it can be charted.
5. Lay unlocks over the table. Look for long gaps, several new systems arriving together, and abilities unlocked after the content that needs them.
6. Compare content supply with demand: how often an activity must repeat to cross each band.
7. Classify gates: level, skill, story, item or time. For each, name what a blocked player can do now.
8. Specify catch-up and anti-farming rules: rested bonus, scaled XP by level difference, one-time sources, and what late joiners get.
9. Simulate the player profiles, including daily and weekly limits, and report where each stalls.
10. For existing players, state how stored XP maps to the new curve so nobody loses a level or unlock without a deliberate decision. List telemetry to verify it.

## Watch out for
- Exponential requirements against roughly linear rewards creating a sudden wall.
- Tuning only for the average player.
- Quest XP being finite while the curve assumes it continues.
- Selling XP boosts and then pacing the free curve to sell them; flag this to the user.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The table shows hours to each milestone for every profile, no unlock gap exceeds the agreed limit, and migration for existing saves is stated.
