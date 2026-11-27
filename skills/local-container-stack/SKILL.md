---
name: local-container-stack
version: 1.0.1
description: >
  Set up a Compose file that runs a project's local databases and services with health checks, safe ports and resettable data. Use when new developers struggle to get dependencies running.
author: Remedy Official
license: Apache-2.0
tags:
  - container tooling
  - devops
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
  library_id: local-container-stack
  official: true
  security_flags: []
---

# Local Container Stack

## When to use
A project needs backing services on a developer machine. Putting the whole editing environment in a container is a separate task.

## Steps
1. Derive services and versions from the code, environment examples, CI and production. Match major versions.
2. Check for existing Compose files and installed tooling (`docker compose version`).
3. Define each service with a pinned image tag. Use service names as hosts between containers; programs on the host use `localhost` and the published port.
4. Publish only needed ports, bound to loopback, for example `"127.0.0.1:5432:5432"`. Make the host port overridable to avoid clashes with locally installed services.
5. Add health checks that prove readiness, such as `pg_isready` for PostgreSQL, using tools present in the image. Use `depends_on` with `condition: service_healthy`, and `service_completed_successfully` for a one-off migration or seed job.
6. Use named volumes for data and check the image's documentation for the data path, which can change between major versions. Add bind mounts for source only when live reload needs them.
7. Provide an example env file with obvious local-only values; ignore the real one. Seed with synthetic data.
8. Put optional services behind profiles.
9. Run `docker compose config` to check the result, noting it prints substituted values, then `docker compose up -d --wait` and an application connection test. Some versions report failure under `--wait` when a one-off job exits and nothing depends on it; run such a job separately with `docker compose run`.
10. Document start, stop, logs and reset. `down` keeps named volumes; `down -v` deletes them, so require confirmation.

## Watch out for
- Database init scripts and password variables applying only to an empty data directory, so later edits seem ignored.
- Changing a database major version over an old volume.
- Image architecture or file sharing differences on Apple silicon and Windows, including line endings in mounted scripts.
- Reusing this file with its weak credentials in production.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A clean start reaches healthy services, the application connects, data survives restart, and reset and port override are documented.
