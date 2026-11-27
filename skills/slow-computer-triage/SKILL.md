---
name: slow-computer-triage
version: 1.0.0
description: >
  Find what is really making a personal computer slow before cleaning, reinstalling or buying. Use when a home laptop or desktop has become sluggish.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - tech-help
  - performance
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: slow-computer-triage
  official: true
  domain: personal
  security_flags: []
---

# Slow Computer Triage

## When to use
Someone's own computer is slow and the cause is unknown.

## Steps
1. Ask when it is slow (startup, browsing, one program, always), since when and what changed. Check a recent backup exists before any change.
2. Observe while it is slow. Use Task Manager, Activity Monitor, or `top` on Linux and note processor, memory, disk and network. Process list from PowerShell: `Get-Process | Sort-Object WorkingSet64 -Descending | Select-Object -First 10`.
3. Check free disk space, and whether the system drive is a spinning disk or solid state.
4. Check drive health with the system's own tools. In PowerShell, `Get-PhysicalDisk` shows health status. Any failing sign means back up first and stop stress testing.
5. Check for heat: loud fan, hot case, slowing under load, blocked vents.
6. Review startup items, browser extensions and unfamiliar programs. Identify each before disabling it.
7. Let pending updates, indexing, sync or an antivirus scan finish, then measure again.
8. Change one thing at a time with a before and after timing. Suggest memory or drive upgrades only where measurements show that limit and the model allows it.

## Watch out for
- "Cleaner", "booster" and driver updater downloads that add problems.
- Deleting system folders or files by guesswork to free space.
- Ending unknown processes, or defragmenting a solid state drive manually.
- Signs of compromise, such as remote tools nobody installed, need a security response, not tuning.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A measured bottleneck is named and the before and after result of the fix is recorded.
