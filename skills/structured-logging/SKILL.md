---
name: structured-logging
version: 1.0.1
description: >
  Convert application logging to structured events with consistent fields, levels, correlation ids and redaction. Use when logs are hard to search or cannot be tied to a request.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - quality
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: structured-logging
  official: true
  security_flags: []
---

# Structured Logging

## When to use
A codebase logs free text or uses print statements, and operators need to filter and correlate.

## Steps
1. Find the logging framework, configuration, current sinks and anything parsing present output. Use the existing framework or its structured formatter.
2. Define a field schema: timestamp in UTC with offset, level, service, version, environment, event name, message, request or trace id, outcome, duration with unit and error details. Follow existing conventions and keep one type per field.
3. Define levels by action: error for a failed operation needing attention, warn for unexpected but handled, info for meaningful state changes, debug for diagnosis and off in normal production.
4. Put values in fields instead of interpolating them into the message. Keep the event name stable.
5. Set context at entry points (HTTP, queue, scheduled job). Accept an incoming id only after checking length and characters, or generate one. Propagate it to outgoing calls.
6. Carry context with the runtime's request-local mechanism and clear it afterward, so pooled threads or async tasks do not inherit another request's data.
7. Log an exception once, at the boundary that handles it, with type, stack and cause.
8. Prevent sensitive data by choosing allowed fields. Do not log whole headers, bodies or objects; add redaction in the formatter as a second layer.
9. Escape through the serializer so user input cannot forge lines. Bound field size, and sample repetitive events without hiding errors or audit records.
10. Migrate one request path, capture output, parse every line, test context isolation under concurrency and redaction with fake secrets, then continue.

## Watch out for
- Libraries or startup crashes writing unstructured lines into the same stream.
- High volume debug or per-item logs inflating cost and slowing hot paths.
- Dynamic keys that overload the log index.
- Breaking dashboards that matched old message text.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Sample output parses, one request can be followed by its id across components, and tests show no context bleed or fake secret leakage.
