---
name: log-pii-redaction
version: 1.0.0
description: >
  Stop secrets and personal data entering application logs, then deal with copies already stored. Use when logs contain tokens, emails, request bodies or other sensitive values.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - privacy
  - logging
kind: native
status: discovered
tools:
  - grep
  - glob
  - read
  - edit
  - bash
metadata:
  source: library
  library_id: log-pii-redaction
  official: true
  domain: security
  security_flags: []
---

# Log Pii Redaction

## When to use
Sensitive values are found, or could easily appear, in logs, traces or error reports.

## Steps
1. List sinks and copies: local files, log platform, tracing, error tracker, proxy access logs, CI output, exports and backups; note retention and who can read each.
2. Search samples for patterns such as authorisation headers, cookies, key prefixes, JWTs, email addresses and password fields. Report counts and locations, not the matched values.
3. If live credentials appear, rotate them first.
4. Trace each leak to its source: request or response dumps, serialised user objects, exception messages, SQL parameters, URLs with tokens, debug level in production.
5. Fix at the call site by logging chosen fields. Use an allow-list for headers and bodies.
6. Add a central redaction processor as a backstop covering nested objects, errors and trace attributes, and a safe string representation for secret types.
7. Where correlation is needed, use an internal ID or keyed hash, not a plain hash of an email, which is easy to guess.
8. Add tests that push unique canary values through success and failure paths and assert they never appear in captured output.
9. With approval, purge or expire existing copies, restrict access meanwhile, and record what cannot be removed.
10. Flag possible notification duties to the privacy or legal owner.

## Watch out for
- Pattern filters miss new formats, encodings and free text.
- Redacting in the log platform is too late for local files and forwarding agents.
- Printing your search hits spreads the data into another log.
- Over-redacting request IDs and error codes destroys debugging value.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Canary tests pass on success and error paths, new production samples are clean, and each historical copy is purged, expiring on a date or documented.
