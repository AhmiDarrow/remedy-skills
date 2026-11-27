---
name: audio-transcription-local
version: 1.0.0
description: >
  Transcribe a recording on the user's own machine and check the weak spots. Use when an interview, memo or meeting recording must become text without uploading it.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - transcription
  - audio
kind: native
status: discovered
tools:
  - bash
  - jobs
  - read
  - write
metadata:
  source: library
  library_id: audio-transcription-local
  official: true
  domain: docs
  security_flags: []
---

# Audio Transcription Local

## When to use
The user has an audio or video file they are entitled to transcribe and wants it kept local.

## Steps
1. Confirm the recording was made with whatever consent applies where it was made; if unsure, ask before continuing.
2. Check which speech-to-text engine is installed (for example whisper.cpp or a Whisper-family package) and read its `--help`; flags differ between builds. Ask before installing one or downloading a model.
3. Inspect the file with `ffprobe`. If the engine needs it, convert with `ffmpeg -i in.m4a -ar 16000 -ac 1 out.wav`.
4. Test a 2 to 3 minute excerpt first to check language, accuracy and speed. Choose a larger model if names and terms are badly wrong.
5. Run the full file through `jobs` with timestamped output. Set the language explicitly if known.
6. Collect a glossary of names and jargon from the user, then search the output for likely misspellings.
7. Review repeated lines, sudden fluent text over silence or music, and gaps against the audio duration.
8. Keep the raw output unchanged and edit a copy, marking `[inaudible 12:34]` instead of guessing.

## Watch out for
- Models can invent plausible sentences during silence or noise.
- Speaker separation is not included in every engine. Do not assign speakers by guesswork.
- Numbers, drug names and negations need an audio check before anyone relies on them.
- Transcripts inherit the recording's sensitivity; do not save them to a synced or shared folder without asking.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A timestamped transcript covers the full duration, with uncertain passages marked and the raw output preserved.
