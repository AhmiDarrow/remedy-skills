---
name: algorithmic-complexity
version: 1.0.1
description: >
  Find accidentally quadratic or worse code, prove it by scaling the input, and fix it with a better data structure or batching. Use when something is fine on small data and crawls on large data.
author: Remedy Official
license: Apache-2.0
tags:
  - perf
kind: native
status: discovered
tools:
  - read
  - grep
  - bash
  - edit
metadata:
  source: library
  library_id: algorithmic-complexity
  official: true
  security_flags: []
---

# Algorithmic Complexity

## When to use
Runtime grows much faster than input size, or a review finds nested work over collections.

## Steps
1. Establish realistic and worst-case sizes. Quadratic work on a list that is always ten long is not worth changing.
2. Time or count operations at n, 2n and 4n on the same shape of data. Roughly doubling suggests linear; quadrupling suggests quadratic. Profile to find which code produces the growth.
3. Look for hidden loops: membership tests or `find` on lists inside a loop, removing or inserting at the front of an array, string or array copying on every iteration (including spread in a reducer), sorting inside a loop, repeated linear regex scans, and a query or request per item.
4. Match the fix to the access: set or map for lookup, group once then join, sort then two pointers or binary search, heap for repeated minimum, deque for queues, builder or join for strings, one batched query.
5. Check semantics the old code had: order, duplicates and which match wins, equality and key normalisation, and mutation during iteration.
6. Consider memory cost and index invalidation; cache only within a scope where the data cannot change.
7. Compare old and new outputs on edge and randomised inputs, then repeat the scaling measurement.

## Watch out for
- Converting to a set inside the loop keeps it quadratic.
- Object keys can silently turn numbers and strings into the same key.
- Hash structures with attacker-chosen or adversarial keys may not give typical-case performance.
- A faster algorithm can lose at small sizes; check the realistic range.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Measurements at several sizes show the improved growth, outputs match the old behaviour, and any memory trade-off is stated.
