---
name: audio-loudness-normalize
version: 1.0.0
description: >
  Normalize audio to a target loudness and true peak with two-pass ffmpeg loudnorm. Use when episodes or videos play too quiet, too loud or uneven against each other.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - audio
  - ffmpeg
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: audio-loudness-normalize
  official: true
  domain: content
  security_flags: []
---

# Audio Loudness Normalize

## When to use
Finished audio must meet a delivery loudness.

## Steps
1. Get the destination's current spec: integrated LUFS and maximum true peak. Broadcast, podcast and streaming targets differ; do not assume one.
2. Check the source for clipping and probe sample rate and channels. Normalising does not repair clipped audio.
3. Measure: `ffmpeg -i in.wav -af loudnorm=I=-16:TP=-1.5:LRA=11:print_format=json -f null -` with your targets.
4. Read `input_i`, `input_tp`, `input_lra`, `input_thresh` and `target_offset` from the output.
5. Second pass: add `measured_I`, `measured_TP`, `measured_LRA`, `measured_thresh`, `offset` and `linear=true` to the same filter.
6. Set `-ar 48000` or the required rate, since loudnorm can output a much higher sample rate.
7. Check the summary's normalization type. It falls back to dynamic when linear gain cannot meet the targets, which changes dynamics.
8. Measure the output again and listen to the loudest and quietest parts.

## Watch out for
- One-pass use on a file when two passes are possible.
- Normalising individual clips of one conversation separately and expecting them to sound matched in context.
- Repeated lossy encodes; work from the highest quality source.
- Raising noise along with quiet speech.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A fresh measurement is within about 1 LU of target, true peak is under the limit, and sample rate is correct.
