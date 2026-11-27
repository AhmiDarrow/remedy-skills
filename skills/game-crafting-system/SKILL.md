---
name: game-crafting-system
version: 1.0.1
description: >
  Design a crafting system with data-driven recipes, discovery, stations, material flow, usable queues and checks for infinite-profit loops. Use when adding or reworking crafting in a game.
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
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: game-crafting-system
  official: true
  domain: gaming
  security_flags: []
---

# Game Crafting System

## When to use
Players turn gathered materials into items, and the system needs design or repair.

## Steps
1. State what crafting is for here: preparation, expression, progression or a resource sink. Cut features that serve none of these. Check how crafted gear compares with drops and shop items.
2. Define recipes as data: stable id, inputs, outputs, station, skill or unlock gate, time, success rule and by-products.
3. Decide discovery (taught, found, experimentation) and ensure required recipes cannot be missed forever. Experiments should not silently destroy rare materials.
4. Give every material at least one source and one use at each stage it drops; flag orphans and bottlenecks.
5. Treat recipes plus buy, sell and salvage prices as a graph. Write a script to search for cycles that return more value or materials than they consume, including bonuses and discounts.
6. Estimate play time to craft key items from gather rates, including inventory limits.
7. Design the interface: search, filter by craftable, show have and need, trace where a missing part comes from, craft in quantity, queue and cancel with defined refunds, and confirm before consuming equipped or protected items.
8. Make consume-and-grant one atomic operation, validated on the server in online games. Handle full inventory, disconnect and save during a queue.
9. Plan tests and measures: recipes never used, materials hoarded, time to key items.

## Watch out for
- Deep intermediate chains that add clicks without decisions.
- Random failure that destroys rare inputs, inviting save reloading.
- If materials can be bought with real money, random outcomes may raise legal and platform issues that need review.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The recipe table validates (no missing sources or unintended profit loops), and discovery, failure, inventory and interface rules are written with estimates marked untested.
