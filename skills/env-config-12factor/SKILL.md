---
name: env-config-12factor
version: 1.0.1
description: >
  Move scattered or hard-coded settings into environment configuration that is typed and validated at startup without changing behaviour. Use when config differs by environment or secrets sit in code.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - config
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: env-config-12factor
  official: true
  security_flags: []
---

# Env Config 12Factor

## When to use
Settings are hard-coded, read ad hoc across the code, or missing values fail only at runtime.

## Steps
1. `grep` for environment reads, config files, literal URLs, ports, keys, passwords and branches on environment name. Include CI, container files and deploy manifests.
2. Make a table: name, consumer, type, required, safe default, secret or not, build time or run time. Record today's effective value source and precedence so behaviour can be preserved, without printing secret values.
3. Create one config module that reads the environment once, parses and validates, and passes typed values onward.
4. Parse strictly. The string `"false"` is truthy in many languages; treat empty strings, bad numbers and unknown enum values as errors.
5. Report all invalid or missing variables at startup together, by name only. Never give secrets or production endpoints a fallback default.
6. Add `.env.example` with placeholders, confirm real env files are ignored by version control and excluded from container build contexts.
7. Update every deployment target with new names before the code requires them, or accept old names for one release.
8. If a secret was ever committed or shipped in a build, tell the user it must be rotated; removing the line is not enough.
9. Test startup with a complete set, each required value missing, and malformed values.

## Watch out for
- Front-end build variables are baked into the bundle and public; no secret belongs there.
- Importing config at module load can break tools and tests that need no database.
- Dumping the whole environment into logs or crash reports.
- Env files override rules vary by library; check the one in use.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
All settings are read through the validated module, a missing required value stops startup naming it, deploy definitions are updated, and no secret value is in tracked files.
