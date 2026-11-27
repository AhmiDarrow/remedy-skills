---
name: spoken-audio-cleanup
version: 1.0.0
description: >
  Clean a voice recording by treating noise, rumble, clicks and level swings in a safe order. Use when a podcast, interview or voiceover sounds noisy or uneven.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - audio
  - podcast
kind: native
status: discovered
tools:
  - bash
  - read
  - write
metadata:
  source: library
  library_id: spoken-audio-cleanup
  official: true
  domain: content
  security_flags: []
---

# Spoken Audio Cleanup

## When to use
Speech is usable but distracting to listen to.

## Steps
1. Keep the original. Work in lossless WAV on copies.
2. Listen and name each problem with timestamps: rumble, hum, hiss, clipping, echo, plosives, crosstalk, level jumps. Only treat what is present.
3. With separate tracks per speaker, process each before mixing.
4. Remove rumble with a gentle high-pass, for example ffmpeg `highpass=f=80`; check it does not thin a deep voice.
5. Treat steady noise lightly with a denoiser such as ffmpeg `afftdn`, or an editor's noise-profile tool using a silent stretch.
6. Tame level swings with moderate compression, then de-ess only if needed.
7. Edit out mistakes after cleanup is chosen, leaving natural breaths and room tone in gaps.
8. Set final loudness last.
9. A/B the same 30 seconds before and after at matched volume, on headphones and a small speaker.

## Watch out for
- Heavy noise reduction that makes voices watery or swallows word endings.
- A hard gate that makes background noise pump in and out.
- Promising to remove room echo or restore clipped speech; recommend re-recording when possible.
- Cutting words so the speaker's meaning changes.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The listed problems are reduced in a level-matched comparison, no words are damaged, and the untouched original remains.
