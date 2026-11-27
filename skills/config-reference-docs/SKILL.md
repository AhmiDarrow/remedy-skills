---
name: config-reference-docs
version: 1.0.0
description: >
  Document every configuration key and environment variable with type, default and effect. Use when users must read source code to configure an application.
author: Remedy Official
license: Apache-2.0
tags:
  - docs
  - config
  - reference
kind: native
status: discovered
tools:
  - grep
  - glob
  - read
  - write
metadata:
  source: library
  library_id: config-reference-docs
  official: true
  domain: docs
  security_flags: []
---

# Config Reference Docs

## When to use
Settings are spread across loaders, schemas and `getenv` calls with no single list.

## Steps
1. Find the load points: schema or settings classes, environment lookups in each language used, deployment manifests and example files.
2. Search for bypasses where code reads the environment directly outside the loader.
3. For each key record name, type, default, required or not, allowed values or range, unit, and what reads it.
4. Determine precedence between sources and whether a change needs a restart.
5. Mark secrets, and show only obvious placeholders for them.
6. Describe the effect of the setting, not its name restated: what the user observes when raising or lowering it.
7. Note interactions, such as a key ignored unless another is enabled, and deprecated aliases.
8. Provide a minimal working example and a production-oriented one, then parse both with the real loader if that can run safely.

## Watch out for
- Reporting the example file's value as the default. The code decides.
- Ambiguous units (`timeout: 30`) and booleans where the string "false" is truthy.
- Reading values from a live `.env` into the docs.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every key found in code appears once with type, default and effect, secrets show placeholders, and unused keys in example files are reported.
