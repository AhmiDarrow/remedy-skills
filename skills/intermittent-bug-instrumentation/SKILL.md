---
name: intermittent-bug-instrumentation
version: 1.0.0
description: >
  Add targeted logging and assertions to catch a rare failure the next time it happens. Use when a bug appears seldom in real use and cannot be reproduced on demand.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - debugging
  - observability
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - write
metadata:
  source: library
  library_id: intermittent-bug-instrumentation
  official: true
  domain: tooling
  security_flags: []
---

# Intermittent Bug Instrumentation

## When to use
You have a handful of sightings, no reproduction, and each new occurrence is precious.
## Steps
1. Collect all past sightings with times, versions and surrounding log lines. Note what they share: uptime, time of day, resume from sleep, data size.
2. List the candidate causes and, for each, the one observation that would confirm it. Instrument for those observations only.
3. Add assertions on invariants at the earliest point they could break, so the report points at the cause and not the later crash.
4. Include correlation data on each line: operation id, thread or task id, sequence number, old and new state, durations from a monotonic clock.
5. If volume is high, keep a fixed-size in-memory ring buffer and write it out only when the assertion fires.
6. Make capture survive the failure: flush on fatal paths, keep logs across restarts and rotation. Enable crash dumps only with the user's agreement: they copy process memory, which can hold passwords and user content, so keep them local, access-restricted and deleted after diagnosis.
7. Never record credentials, tokens or user content; log ids, sizes and hashes.
8. Test the instrumentation by forcing the condition once and reading the output.
9. Write down what each possible result will mean and where to look, then remove the probes after diagnosis.
## Watch out for
- Logging inside a tight loop so heavily that timing changes and the bug hides.
- Instrumentation that ships only in debug builds while the bug occurs in release builds.
- Catch-and-log code that now swallows the error it was meant to observe.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A forced trigger shows the new capture records enough to discriminate between the listed causes, and it is present in the build where the bug occurs.
