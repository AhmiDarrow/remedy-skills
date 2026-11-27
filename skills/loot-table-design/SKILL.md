---
name: loot-table-design
version: 1.0.1
description: >
  Design or audit game loot tables with explicit weights, bad-luck protection, duplicate rules and simulated outcomes. Use when tuning drops, chests or randomised rewards.
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
  library_id: loot-table-design
  official: true
  domain: gaming
  security_flags: []
---

# Loot Table Design

## When to use
Drops need designing, players report droughts or floods, or randomised rewards need their real odds worked out.

## Steps
1. Read the existing tables and the roll code. Determine whether entries are relative weights or independent chances, whether rolls are with replacement, and in what order guarantees, luck modifiers and filters apply.
2. Set targets in player terms per rarity: kills, runs or minutes to first drop and to the full set.
3. Structure tables in layers: first roll a category or rarity, then an item within it, so adding an item does not change rarity odds.
4. Compute the distribution, not just the average. For chance p, getting nothing in n tries is (1-p)^n; at 1% about 37% of players still have nothing after 100 tries.
5. Choose bad-luck protection: hard guarantee at N, rising chance after a threshold, or shuffled bag. Specify where the counter is stored, what resets it, whether it carries between banners or chests, and recompute the effective rate.
6. Decide duplicates: allowed, rerolled, removed from the pool or converted to currency. For complete sets, calculate the cost of the last item.
7. Simulate many players with a script using the game's rules and a fixed seed. Report median, 90th and 99th percentile attempts.
8. For online games, roll on the server and log table version with each drop. If rolls can be bought with real or purchasable currency, tell the user that odds disclosure, age and gambling rules vary by country and platform and need checking before release. Published odds must match the code.

## Watch out for
- Empty pools after level or ownership filters; define the fallback.
- Reloading a save to reroll; persist the seed or result if that matters.
- Integer truncation or float cumulative sums making the last entry unreachable.
- Pity counters that reset on logout or a table update.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tables validate with no empty or unreachable entry, simulated percentiles meet the targets or the gap is stated, and pity and duplicate rules are written down.
