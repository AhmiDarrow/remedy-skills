---
name: macos-launchd-job
version: 1.0.0
description: >
  Create or debug a macOS launchd agent or daemon with the right domain, plist keys, launchctl commands and logs. Use when a script must run on a Mac at login, boot or on a schedule.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - macos
  - automation
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
metadata:
  source: library
  library_id: macos-launchd-job
  official: true
  domain: ops
  security_flags: []
---

# Macos Launchd Job

## When to use
Something needs to run automatically on macOS, or an existing job does not.

## Steps
1. Choose the domain: a LaunchAgent in `~/Library/LaunchAgents` runs in the user's session; a LaunchDaemon in `/Library/LaunchDaemons` runs at boot as root or a named user without GUI access.
2. Write a plist with a unique `Label` and `ProgramArguments` as an array of absolute path plus separate arguments.
3. Set the trigger: `RunAtLoad`, `KeepAlive`, `StartInterval`, `StartCalendarInterval` or `WatchPaths`.
4. Add `WorkingDirectory`, needed `EnvironmentVariables`, `StandardOutPath` and `StandardErrorPath`. There is no shell expansion of `~` or `$HOME` in these values.
5. Validate with `plutil -lint`. Daemon files must be owned by root and not writable by others.
6. Load with `launchctl bootstrap gui/$(id -u) <plist>` for an agent, or `sudo launchctl bootstrap system <plist>` for a daemon.
7. Force a run with `launchctl kickstart -k <domain>/<label>` and inspect `launchctl print <domain>/<label>` for state and last exit code.
8. After edits, `bootout` and bootstrap again.
9. Test through the real trigger, including after logout or reboot.

## Watch out for
- The default PATH is minimal, so Homebrew tools are not found unless referenced fully.
- Privacy protections can deny a background job access to Documents, Desktop, removable or network volumes even though it works in Terminal.
- A program that forks into the background looks exited to launchd and may be killed or relaunched.
- `KeepAlive` on a quickly exiting script causes a throttled restart loop.
- Interval jobs do not run while the Mac sleeps; calendar and interval behaviour after wake differ.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The job runs from its intended trigger with exit code 0, output appears in the log, and it is still loaded after the relevant restart.
