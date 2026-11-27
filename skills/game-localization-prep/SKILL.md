---
name: game-localization-prep
version: 1.0.1
description: >
  Prepare a game for translation: stable string keys, plural and gender handling, fonts, text expansion, voice scripts and pseudo-localization. Use before sending game text or audio to translators.
author: Remedy Official
license: Apache-2.0
tags:
  - gaming
  - i18n
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
  library_id: game-localization-prep
  official: true
  domain: gaming
  security_flags: []
---

# Game Localization Prep

## When to use
A game will ship in more languages.

## Steps
1. Use the engine's localization system. Search code, scenes, data tables, dialogue tools, prefabs, platform text such as achievements and store entries, and text baked into textures or video.
2. Assign stable keys that do not depend on the source wording. Keep player names, chat and ids out of translation.
3. Replace concatenation with whole messages and named placeholders. Handle plurals and grammatical gender through the system's rules, including player and item names that change surrounding grammar.
4. Export context per string: speaker, listener, screen, placeholder meaning, maximum length, screenshot. Add a glossary and do-not-translate list.
5. Pick fonts and fallbacks covering target scripts. Check dynamic glyph atlases or subsets, line breaking for Chinese, Japanese, Korean and Thai, and shaping plus right-to-left layout if targeted.
6. Make layouts flex. Allow at least 30% longer text, far more for very short labels.
7. Run pseudo-localization with accents, padding and markers, then play every screen to find literals, clipping and missing glyphs.
8. Link voice lines to subtitle keys with performer notes, timing limits and lip-sync needs; track which audio matches which text revision.
9. Automate checks for missing keys and placeholder or markup mismatches.
10. Plan in-game review by native speakers and test saves across a language switch.

## Watch out for
- Saving translated names in save files instead of ids.
- Locale-dependent parsing: a comma decimal separator breaking data loading.
- Casing functions that depend on locale altering internal ids.
- Assuming subtitle timing from the source language fits all dubs.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A pseudo-localized playthrough shows no untranslated, clipped or missing-glyph text outside a listed set, and the translator package has keys, context and glossary.
