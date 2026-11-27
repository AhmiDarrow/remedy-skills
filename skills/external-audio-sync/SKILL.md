---
name: external-audio-sync
version: 1.0.0
description: >
  Sync separately recorded audio to camera footage and correct offset and clock drift. Use when a lavalier or recorder track must replace the camera's scratch sound.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - video
  - audio
  - sync
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: external-audio-sync
  official: true
  domain: content
  security_flags: []
---

# External Audio Sync

## When to use
Picture and good sound were captured on different devices.

## Steps
1. Probe both: durations, sample rates and whether video frame rate is constant.
2. Find a shared sharp event near the start, such as a clap, and another near the end.
3. Measure the offset at each from waveforms, or by cross-correlating short extracted excerpts at the same sample rate.
4. If both offsets agree, delay or trim once. In ffmpeg, `-itsoffset` before an input shifts it: `ffmpeg -i video.mp4 -itsoffset 0.42 -i voice.wav -map 0:v -map 1:a -c:v copy -c:a aac out.mp4`.
5. Use a positive value when the external audio must start later; trim its head with `-ss` when it must start earlier.
6. If offsets differ, compute the speed ratio from the time between the two events on each device and apply a tiny correction with `atempo` or a resampler.
7. For stop-start recordings, sync each segment.
8. Verify lips and consonants at beginning, middle and end.

## Watch out for
- Fixing drift with a single offset.
- Variable frame rate footage causing wandering sync; convert to constant frame rate first.
- Getting the sign backwards; test on a short excerpt.
- Accidentally mixing in the scratch track, producing an echo.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Sync holds at three points across the full length and only the intended audio is mapped.
