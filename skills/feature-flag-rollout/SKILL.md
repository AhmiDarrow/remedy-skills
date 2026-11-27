---
name: feature-flag-rollout
version: 1.0.1
description: >
  Put a change behind a default-off flag with server-side enforcement, staged exposure, abort thresholds and a dated removal. Use when shipping a feature gradually or needing a way to switch it off.
author: Remedy Official
license: Apache-2.0
tags:
  - product
  - release
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: feature-flag-rollout
  official: true
  security_flags: []
---

# Feature Flag Rollout

## When to use
A change should reach users gradually, or be reversible without a redeploy.

## Steps
1. `grep` for the existing flag system and copy its naming, evaluation and test patterns. Add a new service or library only if none exists and the user agrees.
2. Write the flag record: name, owner, type (temporary release flag or permanent kill switch), default, removal date or condition.
3. Make off the default in code too, so a missing key, timeout or unreachable flag service gives the old behaviour.
4. Enforce on the server: endpoints, jobs, consumers and emails the feature triggers. Gate the interface too, but hiding a button alone protects nothing.
5. Evaluate once per request or session and pass the value down, so one operation never sees both paths. For percentages, bucket on a stable user or account id so people do not flip between versions.
6. Check data compatibility: with the flag switched off again, old code must still read everything the new path wrote. Schema changes ship separately and stay backward compatible.
7. Before exposure, write the stages (internal, a small percentage, wider, all), the minimum time at each, success measures, and abort thresholds compared against the flag-off group.
8. Test both states, plus turning it off halfway through a multi-step flow.
9. Create the removal ticket now. Ask before changing any production flag value.

## Watch out for
- Client-side flag payloads can reveal unreleased feature names and targeting rules, including email lists.
- A kill switch that only takes effect after a long cache lifetime or an app restart is not a kill switch; time how long it takes.
- Released mobile and desktop builds keep their old flag code for months, so keys they read cannot be deleted or repurposed.
- Reusing an old flag name can revive stale targeting.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Both states pass tests, the off path works with the flag service unavailable, and stages, abort thresholds, owner and removal condition are written down.
