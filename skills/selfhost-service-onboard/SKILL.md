---
name: selfhost-service-onboard
version: 1.0.0
description: >
  Evaluate and deploy a new self-hosted service with pinned versions, persistent data, restricted exposure, backups and an exit path. Use when adding an application to a homelab or personal server.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - selfhost
  - containers
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - web.fetch
metadata:
  source: library
  library_id: selfhost-service-onboard
  official: true
  domain: ops
  security_flags: []
---

# Selfhost Service Onboard

## When to use
Someone wants to run a new app on their own hardware and keep it.

## Steps
1. Confirm the need, who uses it, and whether it holds data they cannot lose.
2. Check the official project: maintenance activity, security advisory history, licence, upgrade notes, resource needs and the official image or package source.
3. Read the example deployment before using it. Question privileged mode, host networking, the container engine socket, broad host mounts and bundled auto-updaters.
4. Pin a specific version. Keep compose or unit files in version control, with secrets in a separate untracked file with tight permissions.
5. List every persistent path and confirm each is mounted; anything unmounted disappears on recreation.
6. Set a non-root user where supported, resource limits, health check, restart policy and log rotation.
7. Bind to private interfaces first. Complete setup before any exposure, because many apps let the first visitor create the admin account. The user sets passwords.
8. Decide access: LAN or VPN by default; public only with TLS, strong authentication and a patch plan.
9. Add data and database to backups and restore them into a throwaway instance.
10. Record URL, version, data paths, upgrade steps, how to export data and how to remove it.

## Watch out for
- Default credentials and sample secrets are public knowledge.
- Ports published by Docker can be reachable despite a ufw rule.
- Mounting the engine socket effectively gives the app control of the host.
- A floating latest tag can perform an irreversible database migration on a routine restart.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The service survives recreation with data intact, is reachable only as intended, has a tested restore and a short operations note.
