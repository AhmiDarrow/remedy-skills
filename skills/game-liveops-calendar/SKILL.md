---
name: game-liveops-calendar
version: 1.0.1
description: >
  Plan a live-game event calendar with goals, content lead times, reward budgets, time zones, kill switches and reviews. Use when scheduling seasonal, weekly or limited-time events.
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
  library_id: game-liveops-calendar
  official: true
  domain: gaming
  security_flags: []
---

# Game Liveops Calendar

## When to use
A running game needs events planned ahead without burning out the team or the players.

## Steps
1. Collect fixed dates (releases, platform submission, holidays, staff absence), past event results and real production capacity.
2. Give each event one main goal with a measure and baseline, such as returning players or draining a surplus currency.
3. Lay out cadence with quiet gaps and checks for overlap: events competing for the same play time, currency or reward slot.
4. Work backwards per event: design lock, content, localization, testing, platform or store approval, announcement, start, end, grace period. Mark what can ship as server config and what needs a client update.
5. Budget rewards against normal earn rates. Check a typical player can reach the headline reward in the time available.
6. Define times in UTC, convert for announcements, and check daylight-saving changes. Use server time, not the device clock.
7. Specify the edges: joining late, matches spanning the end, unclaimed rewards, leftover event currency, refunds and offline players.
8. Build and test a kill switch and schedule override. State what rollback restores, what compensation applies and who may decide at any hour.
9. Rehearse start and end on a test server with shifted time.
10. Review after each event against the goal and baseline, plus complaints and economy effects; update later events.

## Watch out for
- Back-to-back mandatory dailies and false urgency wear players out; offer catch-up and reruns where possible.
- Crediting an event for a rise caused by a sale or holiday.
- Publishing, notifying players or changing live config without explicit approval.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The calendar shows dates in UTC, owners, lead-time milestones, goals, reward budget and kill switch per event, with capacity conflicts flagged.
