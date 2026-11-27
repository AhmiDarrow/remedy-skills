---
name: systemd-service-create
version: 1.0.0
description: >
  Write a systemd unit that runs a program reliably with an unprivileged user, restart policy, ordering, logging and sandboxing. Use when a script or app must run as a service on Linux.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - linux
  - systemd
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
metadata:
  source: library
  library_id: systemd-service-create
  official: true
  domain: ops
  security_flags: []
---

# Systemd Service Create

## When to use
A process is being run from a terminal, tmux or rc.local and needs to be a proper service.

## Steps
1. Find the exact foreground command, working directory, user, environment, files written, ports and shutdown signal.
2. Create `/etc/systemd/system/<name>.service` (or a user unit under `~/.config/systemd/user/`). Use absolute paths; `ExecStart` is not run by a shell, so pipes, `&&` and redirection do not work.
3. Pick `Type` by behaviour: `exec` for an ordinary foreground process where supported, `notify` only if the program sends readiness, `oneshot` for tasks that finish. Run programs in the foreground instead of daemonising.
4. Run as a dedicated user or with `DynamicUser=yes`, using `StateDirectory=` and `LogsDirectory=` for writable paths.
5. Put secrets in a root-only credentials mechanism or `EnvironmentFile`, not in the unit.
6. Set `Restart=on-failure` with `RestartSec`, and bound crash loops with `StartLimitIntervalSec` and `StartLimitBurst` in `[Unit]`.
7. For network ordering use both `Wants=network-online.target` and `After=` it, while still letting the app retry.
8. Add `NoNewPrivileges=yes`, `ProtectSystem=strict`, `ProtectHome=yes` and `PrivateTmp=yes`, relaxing only what testing requires; `systemd-analyze security <unit>` shows exposure.
9. Run `systemd-analyze verify`, `daemon-reload`, `enable --now`, then read `journalctl -u <name>`. Kill the process once and reboot once.

## Watch out for
- The service environment and PATH differ from your shell; version managers loaded by shell profiles are absent.
- `After=` orders but does not pull a dependency in.
- User services stop at logout unless lingering is enabled.
- Editing without `daemon-reload` runs the old definition.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The service runs as the intended user, restarts after a forced crash, starts after reboot and logs to the journal.
