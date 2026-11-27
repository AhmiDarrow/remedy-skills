---
name: visual-regression-setup
version: 1.0.1
description: >
  Set up screenshot comparison for a few critical screens with deterministic rendering and a reviewed baseline process. Use when CSS or component changes keep breaking layouts unnoticed.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - testing
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: visual-regression-setup
  official: true
  security_flags: []
---

# Visual Regression Setup

## When to use
Appearance matters and ordinary assertions cannot catch the breakage.

## Steps
1. Use the existing visual tool, or the browser runner's screenshot assertion such as Playwright's `toHaveScreenshot`. Ask before sending screenshots to a hosted service.
2. Choose a small set: screens or components with high impact or fragile layout, with the themes, widths, long text, empty and error states that actually break.
3. Generate and compare baselines in one pinned environment, normally the CI container image, because OS, fonts and browser change pixels.
4. Make rendering deterministic: seeded data, frozen time and locale, fixed viewport and scale, self-hosted fonts loaded before capture, animations and caret disabled.
5. Wait for a visible ready condition. Mask only regions that are truly variable.
6. Prefer element screenshots over full pages where that limits noise. Set tolerances as low as repeated unchanged runs allow.
7. Define approval: failures publish expected, actual and diff images; a person inspects them; updates go in the same change with the reason, produced by a documented command.
8. Prove it: run repeatedly with no change, then introduce a small real layout fault and confirm it fails.

## Watch out for
- A tolerance large enough to stop flakes can hide a missing icon or button text.
- Baselines made on a developer's machine fail in CI.
- Masking large areas leaves nothing tested.
- Screenshots must contain test data only.
- Visual checks do not verify behaviour or accessibility.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Unchanged runs pass repeatedly, the planted fault fails with a readable diff, and the update and review steps are documented.
