---
name: release-artifact-verify
version: 1.0.0
description: >
  Verify the published download, package or image itself rather than trusting that the release pipeline passed. Use after publishing or while a release is still a draft.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - release
  - verification
kind: native
status: discovered
tools:
  - bash
  - read
  - grep
  - web.fetch
metadata:
  source: library
  library_id: release-artifact-verify
  official: true
  domain: ops
  security_flags: []
---

# Release Artifact Verify

## When to use
A green pipeline can still publish an empty, stale, unsigned or wrong-platform file.
## Steps
1. Write down expectations first: version, source commit, artifact list per platform, signing, and where users get it.
2. Confirm the tag points at the intended commit (`git rev-parse vX.Y.Z^{commit}` and the remote's tag).
3. Compare the published asset list with expectations: names, no missing platform, sizes plausible against the previous release.
4. With approval for the download, fetch from the public location into a new empty directory, as a user would.
5. Check checksums against the published ones, and verify signatures with the platform's tool (`Get-AuthenticodeSignature` on Windows, `codesign --verify` on macOS, the project's signature scheme elsewhere).
6. List package contents before running: missing files, debug data, tests, env files, keys or developer paths. For packages, inspect what the registry serves.
7. Run it in a clean disposable environment; check the reported version and one core action.
8. Test the update path: the previous version detects, downloads and applies this one. Check update manifests and download links resolve.
9. If something is wrong while still a draft, stop. If public, tell the user the options (withdraw, yank, supersede) and do not silently replace files under the same version.
## Watch out for
- Testing the local build output instead of the downloaded file.
- A machine that already has dependencies installed, hiding missing ones.
- A checksum generated from the same corrupted upload proving only self-consistency.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The publicly served artifact has matching version and integrity checks, clean contents, and a successful run and upgrade, with anything not verified stated.
