---
name: beta-program-run
version: 1.0.0
description: >
  Run a product beta with entry criteria, participant selection, feedback handling and exit gates. Use when a feature needs real users before general release.
author: Remedy Official
license: Apache-2.0
tags:
  - content
  - product
  - release
kind: native
status: discovered
tools:
  - write
  - read
  - todo
  - calendar.create_event
metadata:
  source: library
  library_id: beta-program-run
  official: true
  domain: content
  security_flags: []
---

# Beta Program Run

## When to use
Something is working but unproven outside the team.

## Steps
1. Write the questions the beta must answer, such as setup success, reliability or willingness to keep using it.
2. Set entry criteria: core path works, data loss risks addressed, feature can be disabled, support channel staffed.
3. Pick participants covering the intended segments and environments, not only enthusiasts. Size the group to what the team can actually follow up.
4. Tell them plainly what is unfinished, what data is collected, time asked, and how to leave. Have terms reviewed if needed.
5. Instrument the key actions and errors before inviting.
6. Provide one reporting route and a triage rhythm with severity levels and a promised acknowledgement time.
7. Schedule specific check-ins, since silent participants may have quit.
8. Define exit gates in numbers: activation, crash or failure rate, open severe bugs.
9. Report decision, evidence and what participants will receive next.

## Watch out for
- Running with no end date.
- Equating few bug reports with quality when usage is near zero.
- Letting one active tester set the roadmap.
- No migration path for beta data at release.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Exit gates are evaluated with data and the result is release, extend with reason, or stop.
