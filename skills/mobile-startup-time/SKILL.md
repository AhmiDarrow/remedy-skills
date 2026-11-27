---
name: mobile-startup-time
version: 1.0.0
description: >
  Measure and reduce mobile app cold start time by tracing initialisation up to first useful content. Use when an app is slow to open or a release made launch worse.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - mobile
  - performance
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: mobile-startup-time
  official: true
  domain: frontend
  security_flags: []
---

# Mobile Startup Time

## When to use
Users wait on a splash screen, or startup metrics regressed between versions.

## Steps
1. Define the endpoints: first frame, and the moment real content is usable. Separate cold, warm and hot starts.
2. Measure release builds on a slow physical device, several runs after force stop, and report the median and spread. Android: `adb shell am start -W`, Macrobenchmark startup timing, `reportFullyDrawn()`. iOS: Instruments App Launch template and MetricKit field data.
3. Trace what runs before first content: SDK initialisers, dependency graph construction, content providers added by libraries, static initialisers, dynamic frameworks, synchronous disk, keychain or network calls, large JavaScript bundles.
4. For each item decide: required before first frame, deferrable after it, lazy on first use, or removable.
5. Remove synchronous network waits; show cached content and refresh.
6. Android: consider Baseline Profiles and confirm R8 is on. iOS: reduce dynamic library count and launch-time work. React Native or Flutter: also measure engine start and initial bundle or isolate work.
7. Use the system splash API rather than an extra splash screen with a timer.
8. Change one group at a time, re-measure, and add a regression check or release comparison.

## Watch out for
- Deferring crash reporting hides startup crashes; keep it early and light.
- Moving work just after first frame can make the first tap freeze.
- The launch immediately after install or update is not representative of later cold starts.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Median cold start to usable content on the reference device is reported before and after with run counts, and each remaining pre-content initialiser has a stated reason.
