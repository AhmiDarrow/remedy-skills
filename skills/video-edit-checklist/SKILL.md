---
name: video-edit-checklist
version: 1.0.1
description: >
  Review a video edit in order, from story cut through sound, picture, captions, rights and export verification. Use before approving or publishing a cut, or when planning the finishing passes.
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
  - bash
  - web.search
metadata:
  source: library
  library_id: video-edit-checklist
  official: true
  domain: content
  security_flags: []
---

# Video Edit Checklist

## When to use
A cut exists and needs finishing without polishing footage that will later be removed.

## Steps
1. Collect the goal, audience, destinations, length target, approved script and any client notes. Say whether you can only review documents and file data or have also been given frames or a transcript.
2. Story pass: does the opening state or show the payoff, does each section earn its place, are claims correct. Log notes by timecode. Lock the story before finishing.
3. Pacing pass: trim repeats and dead air, but keep pauses carrying meaning. Cover jump cuts with relevant footage or accept them deliberately.
4. Sound pass: dialogue intelligible on phone speaker and headphones, no clipped words at cuts, music ducked under speech, noise treated lightly, loudness set to the destination's current target.
5. Picture pass: exposure and white balance match across shots, no flash frames, black gaps or offline media, private information in screens and backgrounds blurred and checked frame by frame.
6. Text pass: names and titles verified, readable long enough, inside safe areas. Captions corrected for words, timing, speaker identification and meaningful sounds.
7. Rights pass: licences or permission for music, footage, images, fonts and appearances; sponsorship disclosed.
8. Export to the destination's recommended settings, keeping source frame rate unless required otherwise. Inspect with `ffprobe -hide_banner file.mp4` for resolution, frame rate, codecs, audio channels and duration.
9. Watch the exported file from start to end. Then choose thumbnail stills and archive the project with its assets.

## Watch out for
- Approving from the editing timeline; export glitches only show in the output file.
- Picture or music changes after captions or mix, which silently break sync.
- Overwriting the previous approved export; version filenames.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each pass has timecoded findings marked fixed or open, the exported file's properties match the destination, and someone has watched that exact file through (or this is listed as outstanding).
