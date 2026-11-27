---
name: rtl-layout-support
version: 1.0.0
description: >
  Add right-to-left support to a web interface with logical CSS properties, mirrored icons and isolated mixed text. Use when adding Arabic, Hebrew, Persian or Urdu locales.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - css
  - i18n
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - computer.navigate
  - computer.screenshot
metadata:
  source: library
  library_id: rtl-layout-support
  official: true
  domain: frontend
  security_flags: []
---

# Rtl Layout Support

## When to use
The product will ship in a right-to-left language, or an existing RTL build has misplaced controls and scrambled mixed text.

## Steps
1. Set `dir` and `lang` on the `html` element from the active locale; do not rely on CSS `direction`.
2. `grep` styles for `left`, `right`, `margin-left`, `padding-right`, `text-align: left`, border and radius sides.
3. Convert to logical forms: `margin-inline-start`, `padding-inline-end`, `inset-inline-start`, `text-align: start`, `border-start-start-radius`.
4. Fix what logical properties miss: `translateX`, box shadow offsets, gradients, `transform-origin`, background position, canvas drawing and JavaScript that computes `left`. Multiply by a direction sign.
5. Decide icon mirroring one by one. Back, forward, reply and progress arrows mirror; checkmarks, media play, clocks, logos and most real-world objects do not.
6. Isolate user content with `dir="auto"` or the `bdi` element so Latin names, numbers and punctuation do not reorder surrounding text.
7. Keep inherently left-to-right fields (email, URL, phone, code) as `dir="ltr"`, aligned sensibly.
8. Check arrow keys in sliders, tabs and carousels, and swipe direction.
9. Test with a pseudo-RTL toggle during development, then with real translated text reviewed by a reader of the language.

## Watch out for
- A generic CSS flipping plugin applied on top of logical properties flips things twice.
- `flex-direction: row-reverse` added for RTL reverses again, because rows already follow direction.
- Letter spacing breaks joined scripts; remove it for Arabic text.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every main screen mirrors correctly in an RTL locale, listed non-mirrored icons are unchanged, mixed-direction strings read correctly, and LTR screenshots are unchanged.
