---
name: behavior-spec-from-code
version: 1.0.0
description: >
  Recover a written behaviour spec from existing code and tests when no documentation exists. Use before rewriting, porting or replacing a feature whose rules live only in the source.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - requirements
  - legacy
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
  - write
metadata:
  source: library
  library_id: behavior-spec-from-code
  official: true
  domain: docs
  security_flags: []
---

# Behavior Spec From Code

## When to use
A rewrite or port is planned and "it should work like the old one" is the entire requirement.
## Steps
1. List entry points: commands, routes, event handlers, scheduled jobs, public functions. Search for registrations rather than trusting folder names.
2. For each, follow the code to every side effect: writes, network calls, messages, logs that other tools parse, exit codes.
3. Extract rules as plain statements with a `path:line` citation: defaults, limits, rounding, sort order, tie-breaking, retries, timeouts.
4. Harvest hidden rules from conditionals with odd special cases, error messages, migrations and existing tests.
5. Use `git log -S` on strange constants to learn why they appeared.
6. Confirm rules you only inferred by running the program on edge inputs, in a disposable copy with test data and with outbound writes, mail and payments disabled or pointed at test services. If that cannot be arranged, mark the rule unverified. Record input and observed output.
7. Tag every rule: intended, probably accidental, or unknown. Do not silently fix apparent bugs in the spec; list them for a keep-or-change decision.
8. Add what the old system does not handle, so the new one does not inherit an unstated expectation.
## Watch out for
- Documenting what function names suggest instead of what the body does.
- Missing behaviour supplied by the framework or database: constraints, cascades, middleware, default encodings.
- Callers that depend on accidental behaviour such as output ordering. Check consumers before declaring something a bug.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every entry point has its rules written with source citations, inferred rules are verified or marked unverified, and questionable behaviours are listed for decision.
