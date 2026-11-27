---
name: symptom-diary-log
version: 1.0.0
description: >
  Set up a consistent symptom diary that a clinician can read at a glance, without interpreting it. Use when someone is tracking a recurring symptom before or between visits.
author: Remedy Official
license: Apache-2.0
tags:
  - personal
  - health
  - tracking
kind: native
status: discovered
tools:
  - read
  - write
  - routines.create
metadata:
  source: library
  library_id: symptom-diary-log
  official: true
  domain: personal
  security_flags: []
---

# Symptom Diary Log

## When to use
A symptom comes and goes and memory will not give a reliable picture.

## Steps
1. Check first for urgent warning signs in what is described; if present or sudden and severe, send them to urgent or emergency care rather than starting a diary.
2. Ask whether a clinician gave a form or named what to track. Use that over any invented one.
3. Choose few fields: date and time, symptom, severity on one defined scale, duration, what they were doing, anything taken and when, effect on sleep, work or activity.
4. Define the scale in plain anchors once, such as 3 means noticeable but carrying on, 7 means had to stop.
5. Record only possible triggers the person or clinician wants watched, as observations.
6. Include good days, so frequency can be seen.
7. Offer a brief daily reminder via `routines.create` after approval, with an end or review date.
8. Before the appointment, produce a summary: number of days with the symptom out of days logged, severity range, time-of-day pattern as counted, notable episodes, and gaps.

## Watch out for
- Filling missed days from memory without labelling them as recalled.
- Declaring that a food or activity causes the symptom; a short diary cannot show that.
- Suggesting stopping or changing medicine or diet as an experiment.
- Tracking that increases worry; offer to reduce frequency and mention it to the clinician.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Entries use the same fields and scale, and a counted one-page summary shows gaps honestly.
