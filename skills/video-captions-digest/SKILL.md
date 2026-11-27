---
name: video-captions-digest
version: 1.0.0
description: >
  Turn a video's captions into a timestamped digest the user can navigate. Use when asked to summarise a talk, lecture or recorded demo without watching it all.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - summaries
  - video
kind: native
status: discovered
tools:
  - read
  - bash
  - web.fetch
  - write
metadata:
  source: library
  library_id: video-captions-digest
  official: true
  domain: docs
  security_flags: []
---

# Video Captions Digest

## When to use
The user wants the substance of a video and a way to jump to the parts that matter.

## Steps
1. Get text through a permitted route: a transcript the page offers, a caption file the user provides, or captions of their own recording. If none exists, ask before transcribing audio they have the right to use.
2. Identify whether captions are human-made or automatic. For automatic ones, expect wrong names, numbers and technical terms.
3. Strip subtitle numbering and rolling duplicate lines from SRT or VTT files, keeping one timestamp every minute or so.
4. Segment by topic shifts, not fixed intervals. Use the video's chapters if present.
5. For each segment give start time, topic and the claim or technique shown.
6. Verify names and key figures against slides, the description or an authoritative page; mark unverifiable ones.
7. Flag moments where meaning depends on the screen ("as you see here"), because the text cannot carry it.
8. Open with a short overview and the two or three timestamps most useful for the user's goal.

## Watch out for
- Captions often lack speaker labels. Do not guess who said what in panels.
- A dropped "not" in automatic captions reverses a claim; check surprising statements against the audio or flag them.
- Do not imply you watched visuals you never saw.
- Sponsor reads and Q&A tangents should not be reported as the talk's findings.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each segment has a real timestamp from the captions, and caption quality and visual gaps are stated.
