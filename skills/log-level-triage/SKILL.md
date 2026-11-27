---
name: log-level-triage
version: 1.0.1
description: >
  Investigate errors in application or server logs by bounding the time window, grouping messages and tracing failing requests. Use when something is failing and the logs are the main evidence.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - debug
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
metadata:
  source: library
  library_id: log-level-triage
  official: true
  security_flags: []
---

# Log Level Triage

## When to use
There is a log file or log system full of noise and a failure to explain. If a live outage needs coordination, run that alongside.

## Steps
1. Pin down the symptom, first known bad time, last known good time, time zone and affected users or hosts. If users are being harmed now, raise mitigation first.
2. Find all relevant sources: application, proxy, database, service manager or orchestrator, and where rotated or previous-container logs live (`journalctl -u <unit> --since <time>`, `kubectl logs <pod> --previous`).
3. Preserve evidence before restarts or rotation, with access restricted.
4. Check coverage: gaps, sampling, ingestion delay, dropped lines, and clock or time zone differences.
5. Group by normalised signature, replacing ids, numbers and addresses. Compare counts with an equal healthy window to find what is new or changed, including messages that stopped.
6. Find the earliest anomaly, including warnings and info lines before the first error. Compare with deploys, config, traffic and scheduled jobs.
7. Follow several failing requests by request or trace id across services, and one successful request for contrast. Read the full stack trace down to the deepest cause.
8. Normalise by traffic and split by host, version, endpoint and tenant to see what the failures share.
9. Separate observed facts from hypotheses. For each hypothesis, say what the logs would show if it were false, and check.
10. Report cause or leading candidates, evidence lines, missing logging and the next test.

## Watch out for
- Chasing the loudest error, which may be old background noise or a retry cascade.
- Trusting the level: real failures are often logged as info, or caught and swallowed.
- Loading huge files whole; filter by time and signature first.
- Copying tokens or personal data from logs into reports.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The failure has a time-bounded evidence chain, rival explanations are ruled out or listed, and remaining gaps have a concrete next check.
