---
name: semver-bump
version: 1.0.1
description: >
  Decide whether a release is major, minor or patch from its effect on users and apply the version consistently. Use before tagging a release or when unsure whether a change is breaking.
author: Remedy Official
license: Apache-2.0
tags:
  - release
  - versioning
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - grep
metadata:
  source: library
  library_id: semver-bump
  official: true
  security_flags: []
---

# Semver Bump

## When to use
A version number must be chosen or bumped.

## Steps
1. Find the last released version from tags and the package registry, which can disagree with files in the tree.
2. Define the public surface: exported APIs, command line flags and output, configuration keys, file and wire formats, environment variables, database schema others read, and supported runtime versions.
3. Diff since that release (`git diff <tag>..HEAD`) and list changes to that surface. Do not rely on commit types alone.
4. Classify under Semantic Versioning: incompatible change is major; backward-compatible functionality or a deprecation is minor; backward-compatible bug fixes are patch. The highest wins.
5. Test borderline cases against a real consumer: new required parameters, stricter validation, changed defaults or error types, removed platforms, new enum values, and raised dependency requirements. Follow the project's stated policy where the answer depends on it.
6. For `0.y.z`, the specification promises no stability, but package managers and the project may treat a minor bump as breaking. Follow that convention. For prereleases, remember `1.0.0-rc.1` sorts before `1.0.0`.
7. Present the proposed version with the evidence for it. If the project does not use Semantic Versioning, follow its scheme.
8. After agreement, use the project's sync script or tool, then search for the old version string and inspect each hit. Note that `npm version` creates a commit and tag by default in a Git repository; use `--no-git-tag-version` if only files should change.
9. Update lock files and the changelog. Tag or publish only when asked, and never force-push or move a published tag without an explicit request.

## Watch out for
- Replacing the old number blindly and changing an unrelated dependency with the same version.
- Reusing a published version; most registries refuse it, and caches may hold the old content.
- Calling a break a patch because it fixes wrong behaviour people depend on without saying so.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The bump is justified by listed surface changes, all version locations agree, and nothing was tagged or published without a request.
