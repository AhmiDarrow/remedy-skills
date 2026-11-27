---
name: regex-dialect-porting
version: 1.0.0
description: >
  Move regular expressions between engines such as PCRE, JavaScript, Python, RE2, POSIX tools and .NET without changing what they match. Use when a pattern fails or differs elsewhere.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - regex
  - cross-platform
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
  - web.fetch
metadata:
  source: library
  library_id: regex-dialect-porting
  official: true
  domain: tooling
  security_flags: []
---

# Regex Dialect Porting

## When to use
A pattern is being copied from one language or tool to another.
## Steps
1. Name both engines and versions, plus the flags and the calling function in each. Full match, search and match-at-start are different operations.
2. First collect fixtures from the source engine: strings that match with their captured groups, and near misses that must not.
3. List the features used: lookaround, backreferences, atomic or possessive groups, recursion, named groups, inline flags and Unicode classes.
4. Check support in the target. RE2-family engines (including Go's regexp) have no backreferences or lookaround; split into two checks or add code. POSIX `grep -E` and `sed -E` lack lazy quantifiers and may lack `\d`.
5. Translate syntax that differs: named group spelling, replacement references (`$1` versus `\1`) and Unicode property escapes, which in JavaScript need the `u` or `v` flag.
6. Check semantics that look identical: whether `\d`, `\w` and `\b` are Unicode-aware, whether `$` matches before a final newline, what dot matches, and what multiline mode means (it differs in Ruby).
7. Account for the host string layer: escape backslashes or use raw literals, and shell quoting.
8. Watch for the JavaScript global or sticky flag keeping `lastIndex` between `test` calls.
9. Run all fixtures in the target engine and compare captures, not just match or no match.
## Watch out for
- Online testers set to the wrong flavor give false confidence.
- Validation patterns need explicit whole-string anchoring; in Python use `fullmatch`.
- A rewrite to avoid lookaround can introduce heavy backtracking in backtracking engines.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All positive, negative and capture fixtures give the intended results in the target engine, with any deliberate differences listed.
