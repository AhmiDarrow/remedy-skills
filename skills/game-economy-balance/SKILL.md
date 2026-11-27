---
name: game-economy-balance
version: 1.0.1
description: >
  Model a game's currency and item sources and sinks per player type, simulate pacing and exploits, and propose reversible tuning changes. Use when players hoard, starve, grind or inflation appears.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - design
  - systems
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: game-economy-balance
  official: true
  domain: gaming
  security_flags: []
---

# Game Economy Balance

## When to use
Resources pile up, run dry or make progress too slow or fast.

## Steps
1. List every currency and key resource with all sources, sinks, converters, caps, expiry and trades, reading actual data and code, including quests, events and refunds.
2. Separate faucets (create), sinks (destroy) and transfers (move between players). A trade removes only its fee or tax.
3. Define player profiles (new, casual, regular, heavy, optimiser) with minutes per day and activities. Label assumptions and replace them with telemetry where available.
4. Model earn and spend per profile over time with a small script or CSV: balances, time to key purchases and sink uptake.
5. Search for loops: buy-sell or craft-salvage profit, stacked discounts, repeatable rewards, alternate-account funnelling, duplication on disconnect.
6. State the target for each problem (such as hours to first upgrade) before choosing numbers.
7. Change the fewest values, show before and after per profile, and test pessimistic and optimistic assumptions.
8. For live games, say what happens to existing balances and items, ship values versioned with a rollback, note that rollback does not undo earned currency, and watch earn, spend, median balance and time-to-goal.

## Watch out for
- Averages hiding that a few heavy players hold most currency while newcomers starve.
- Sinks that feel like punishment, or cuts to things already earned.
- Tuning to push real-money spending through artificial scarcity; flag it, and check disclosure rules and effects on minors.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Sources and sinks are inventoried, per-profile projections reproduce from saved files, exploits are listed, and each proposed change has a target, rollback and metric.
