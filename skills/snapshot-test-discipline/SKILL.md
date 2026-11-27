---
name: snapshot-test-discipline
version: 1.0.1
description: >
  Clean up snapshot tests so each one is small, deterministic and reviewable, replacing opaque ones with explicit assertions. Use when snapshots are huge or routinely updated without reading.
author: Remedy Official
license: Apache-2.0
tags:
  - testing
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
  library_id: snapshot-test-discipline
  official: true
  security_flags: []
---

# Snapshot Test Discipline

## When to use
Serialized-output tests (data or markup, not screenshots) fail often and nobody trusts or reads the diffs.

## Steps
1. List snapshots by size and by how often history shows them changing. Look for commits that update many at once.
2. For each ask what regression it should catch. If nobody can say, check whether other tests cover the behaviour before removing it.
3. Replace logic and interaction checks with explicit assertions on the values, roles or calls that matter.
4. Keep snapshots for stable, intentional output: serializer formats, generated code, error messages, CLI help. Snapshot the smallest relevant part.
5. Remove nondeterminism: fix clock, IDs, locale and ordering, or use field matchers or serializers that normalise only the volatile field.
6. Use small inline snapshots where the runner supports them, so expected output sits beside the test.
7. Make CI refuse to write or accept new snapshots (for Jest, `--ci`; check other runners). Updates are targeted to named tests, and every changed line is reviewed against the intended change.
8. Find obsolete snapshots from a full-run report and remove them, then break one behaviour to confirm the replacement fails.

## Watch out for
- Updating all snapshots to get green records the bug as expected output.
- Over-broad normalisation can erase the very value under test.
- Deleting a snapshot may drop the only coverage of some behaviour.
- Snapshots can capture tokens or personal data and commit them.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Remaining snapshots each have a stated purpose, are stable across repeated runs, and removed ones are replaced or recorded as unneeded.
