---
name: screen-demo-production
version: 1.0.0
description: >
  Plan and record a product screen demo with a short script, clean test data and a clutter-free capture. Use when making a walkthrough or tutorial video of software.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - video
  - demo
kind: native
status: discovered
tools:
  - write
  - read
  - computer.snapshot
  - computer.window
  - computer.screenshot
  - computer.click
  - computer.type
  - bash
metadata:
  source: library
  library_id: screen-demo-production
  official: true
  domain: content
  security_flags: []
---

# Screen Demo Production

## When to use
Software needs to be shown working in a short video.

## Steps
1. State what the viewer can do afterwards and set a target length. One task per video.
2. Write two columns: on-screen action and spoken line. Start with the result, then show how.
3. Prepare a demo account and invented data such as Test User, with the state resettable between takes.
4. Dry run the whole path and note loading waits, bugs and dialogs.
5. Set the capture window to the delivery aspect ratio and make text readable on a phone using in-app or browser zoom. Leave system display settings alone.
6. Silence notifications and close password managers, mail, chats and personal bookmarks.
7. Record a ten-second test and check cursor visibility, text sharpness and microphone level.
8. Record in short scenes, pausing between actions. Record narration separately if that is easier to fix.
9. Review frame by frame around forms, address bars and terminals for secrets. The user publishes.

## Watch out for
- Tokens in terminal history or environment output.
- Faking a feature or hiding errors so the demo shows behaviour users will not get; label sped-up waits.
- Narration saying "click here" with no visible target.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The video completes the stated task within the length target and a full review finds no private data.
