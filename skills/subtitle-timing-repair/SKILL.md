---
name: subtitle-timing-repair
version: 1.0.0
description: >
  Fix subtitle files that are offset, drifting or hard to read by correcting timing, splits and encoding. Use when captions appear early, late or too fast.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - subtitles
  - editing
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: subtitle-timing-repair
  official: true
  domain: content
  security_flags: []
---

# Subtitle Timing Repair

## When to use
An SRT or VTT file does not match its video or reads badly.

## Steps
1. Copy the original and parse cue numbers, times, text and encoding.
2. Measure the error at a line near the start and one near the end against the audio.
3. Same error at both means a constant offset: shift every cue.
4. A growing error means rate mismatch: apply new = a * old + b, solving a and b from the two points. A jump partway means the video edit differs; fix each segment separately.
5. Do the arithmetic with a script in milliseconds. SRT uses a comma decimal separator; WebVTT uses a period and starts with `WEBVTT`.
6. Check for negative times, end before start, and overlaps.
7. For readability, a common house style is up to two lines of about 42 characters and roughly 17 to 20 characters per second; follow the client's spec if there is one.
8. Split at phrase boundaries, then spot-check early, middle and end.

## Watch out for
- Using one offset to fix drift, which only matches one moment.
- Losing accented characters by saving in the wrong encoding.
- Shortening speech to hit reading speed in a way that changes meaning.
- Breaking style tags or positioning while rewriting cues.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Spot checks at three or more points match the audio, the file parses with no overlaps, and the original is preserved.
