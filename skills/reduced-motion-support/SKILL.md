---
name: reduced-motion-support
version: 1.0.0
description: >
  Add reduced-motion support that removes harmful movement while keeping feedback, across CSS, script, video and canvas. Use when an app animates heavily or ignores the system motion setting.
author: Remedy Official
license: Apache-2.0
tags:
  - frontend
  - animation
  - accessibility
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
  library_id: reduced-motion-support
  official: true
  domain: frontend
  security_flags: []
---

# Reduced Motion Support

## When to use
Parallax, zooms, auto-playing motion or large slides run regardless of the user's preference.

## Steps
1. Inventory motion from every source: CSS transitions and keyframes, animation libraries, smooth scrolling, canvas and WebGL, vector animation players, GIFs and autoplay video.
2. Sort each: essential to meaning, helpful feedback, or decoration.
3. Define the replacement per kind. Large movement, scaling, spinning, parallax and scroll-linked effects become instant changes or short fades. Small state feedback such as color or opacity can stay. Progress indication must remain perceivable.
4. In CSS use `@media (prefers-reduced-motion: reduce)`, or better, add motion only inside `no-preference`.
5. In script use `matchMedia`, subscribe to changes, and put the check in one shared helper or the animation library's global option.
6. Disable smooth `scrollIntoView` and automatic carousel advance.
7. Provide pause or stop controls for moving content that starts automatically and lasts more than five seconds, independent of the preference.
8. Audit flashing: nothing should flash more than three times per second.
9. Emulate the setting in dev tools and walk the inventory. For the real operating system setting, ask the user to toggle it and report; do not change it yourself.

## Watch out for
- A blanket rule setting all durations to zero can break code waiting for `animationend` or `transitionend` and removes useful cues.
- Server rendering cannot know the preference, so CSS should carry the initial behaviour.
- A static spinner with no text looks frozen.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
With the preference on, each inventory item shows its planned replacement, all flows still complete, and toggling the setting takes effect without breaking state.
