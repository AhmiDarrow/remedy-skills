---
name: mobile-screen-reader-pass
version: 1.0.0
description: >
  Test and fix a mobile app with VoiceOver and TalkBack, covering labels, order, custom controls and announcements. Use when an app needs accessibility checks on real devices.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
  - mobile
  - accessibility
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - todo
metadata:
  source: library
  library_id: mobile-screen-reader-pass
  official: true
  domain: testing
  security_flags: []
---

# Mobile Screen Reader Pass

## When to use
Custom-drawn or cross-platform screens need to work with iOS and Android screen readers.

## Steps
1. Select the critical tasks. If you cannot operate a device, give the user a script and record what they hear; code inspection alone is not a pass.
2. Enable a quick toggle shortcut first, so the tester can turn the reader off again.
3. Swipe through each screen in order, then try explore by touch. Note unlabelled controls, raw file names, silent elements, duplicate stops and wrong order.
4. Group related content into one stop, such as a list card, using the platform's merge semantics, and expose secondary buttons as custom actions.
5. Give every control a concise name without the role word, plus correct role, state and value. SwiftUI uses `accessibilityLabel`, `accessibilityValue` and traits; Compose uses semantics and `contentDescription`; React Native and Flutter have their own semantics properties.
6. Hide decorative images.
7. Make custom sliders, charts and gesture-only actions operable through adjustable or custom actions.
8. On modals, trap reader focus inside and return it on close. Announce important async results.
9. Also check enlarged text and voice control labels, and run Xcode's Accessibility Inspector or Android's Accessibility Scanner as a supplement.
10. Retest failures on both platforms.

## Watch out for
- A fix correct on one platform can double-announce on the other.
- Tappable plain views often have no button role.
- Hints are optional speech and may be off; essential information belongs in the label or value.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each selected task has been completed with both readers from actual device observations, or the untested platform and remaining failures are stated.
