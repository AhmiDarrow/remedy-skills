---
name: video-chapter-markers
version: 1.0.1
description: >
  Create accurate, scannable video chapters from a timed transcript, edit timeline or notes, formatted for the destination. Use when a long video, stream or webinar needs timestamps and chapter titles.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - video
kind: native
status: discovered
tools:
  - read
  - write
  - web.search
metadata:
  source: library
  library_id: video-chapter-markers
  official: true
  domain: content
  security_flags: []
---

# Video Chapter Markers

## When to use
Viewers need to jump to parts of a longer video.

## Steps
1. Get a timed source: caption file, timestamped transcript or exported edit markers, plus the final duration. An outline without times can give titles only, so ask for timing rather than estimating it.
2. Confirm the timings match the published cut. Added intros, trimmed pauses or inserted ads shift everything; check a few points near the start, middle and end.
3. Mark where the subject or task changes, not at fixed intervals. Aim for the number a viewer can scan.
4. Place each marker where the new section really begins, just before its first sentence or title card, not at the first keyword mention.
5. Title each by what the viewer gets ("Fix the export error"), short, specific, in a consistent grammatical form. Put distinctive words first.
6. Check the destination's current rules with `web.search`. For YouTube description chapters, the list must start at 00:00, hold at least three timestamps in ascending order, and each chapter must last at least 10 seconds.
7. Format one per line as time then title, using one consistent time format and hours once the video passes 60 minutes.
8. Validate: ascending order, no duplicates, minimum lengths including the last chapter, nothing beyond the duration.
9. If a different format is needed (WebVTT chapter track, player metadata, editor markers), produce it with matching start and end times.

## Watch out for
- Timestamps taken from the raw recording rather than the final export.
- Titles that promise a topic only mentioned in passing, or that reveal a result the creator wants withheld.
- Automatic captions garble names used in titles; verify spellings.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A paste-ready list passes the destination's rules, its times were checked against the final cut (or are clearly marked unverified), and titles describe their sections accurately.
