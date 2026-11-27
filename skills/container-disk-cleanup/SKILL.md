---
name: container-disk-cleanup
version: 1.0.0
description: >
  Reclaim disk used by a container engine by identifying images, build cache, logs and volumes before pruning anything. Use when a Docker or compatible host is running out of disk.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - containers
  - storage
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
metadata:
  source: library
  library_id: container-disk-cleanup
  official: true
  domain: ops
  security_flags: []
---

# Container Disk Cleanup

## When to use
A build server or container host is filling up and the engine's data directory is the suspect.

## Steps
1. Confirm which host and engine context you are on, then run `docker system df -v` and check the filesystem holding the data root.
2. Compare with real disk usage. Large container logs are not clearly shown there; check log file sizes under the data root with elevated read access.
3. List volumes and map each to its containers and compose project. An unused volume may be the only copy of a stopped database.
4. List stopped containers and check whether any hold data in their writable layer.
5. Prune in order of safety, showing the owner what each step removes: build cache (`docker builder prune`), dangling images (`docker image prune`), then unused tagged images (`docker image prune -a`) with an age filter.
6. Remove volumes only individually, by name, after confirming a backup or that the data is disposable.
7. Prevent recurrence: set log rotation, for example `max-size` and `max-file` for the json-file driver in `daemon.json`, and schedule age-filtered cache pruning.
8. Recreate containers so they pick up new log settings; daemon defaults apply only to newly created ones.

## Watch out for
- `docker system prune -a --volumes` is not a routine cleanup; check what the installed version counts as unused.
- Removing an image that exists only locally means it cannot be pulled again.
- Deleting files by hand inside the engine's data directory corrupts its metadata.
- On desktop engines, freed space may not return to the host until the virtual disk is compacted.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Free space is recovered with before and after figures, no needed volume or image was removed, and growth has a limit in place.
