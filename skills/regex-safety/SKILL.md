---
name: regex-safety
version: 1.0.1
description: >
  Review regular expressions that process untrusted input for catastrophic backtracking and wrong matches, then fix and test them. Use when a pattern validates user input or a request pins a CPU core.
author: Remedy Official
license: Apache-2.0
tags:
  - security
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
  library_id: regex-safety
  official: true
  security_flags: []
---

# Regex Safety

## When to use
A regex runs on data an outsider controls: validators, parsers, routes, log processors.

## Steps
1. Find patterns, including ones built from strings, in config and in validation schemas. Note the engine and who controls both input and pattern.
2. Know the engine. Backtracking engines (JavaScript, Python `re`, Java, .NET, PCRE) can blow up; RE2, Go `regexp` and Rust `regex` match in linear time but lack some features.
3. Look for ambiguity: nested quantifiers like `(a+)+`, repeated alternatives that overlap like `(\w|\d)*`, and neighbouring repeats over the same characters like `\s*\s*` or `.*.*=`.
4. Reproduce with a growing run of the repeated character followed by one that forces failure. Time lengths such as 1k, 2k and 4k, starting small, in a local process with a timeout. Quadratic growth matters too, including from unanchored searches.
5. Fix in order of preference: use a parser or string functions; make each character matchable one way; use atomic groups or possessive quantifiers where supported; switch to a linear engine.
6. Enforce a length limit before matching, and a match timeout where the engine offers one.
7. Check correctness: whole-input matching for validators (`fullmatch` or true end anchors, since Python `$` also matches before a final newline), grouped alternations under anchors, escaped dots, and intended Unicode behaviour.
8. Escape user text inserted into a pattern. Do not run user-supplied patterns on a backtracking engine without isolation and limits.
9. Add accept, reject and long adversarial cases to tests.

## Watch out for
- A rewrite that is fast but accepts different strings; compare old and new on a corpus.
- Online testers may use another engine, and pasting private input there leaks it.
- A timeout around a thread does not stop every engine; verify the work really ends.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Each risky pattern is fixed or bounded, adversarial input at the length limit finishes within the stated budget, and match tests pass.
