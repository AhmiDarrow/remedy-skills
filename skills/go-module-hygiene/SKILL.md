---
name: go-module-hygiene
version: 1.0.1
description: >
  Clean up a Go module's go.mod and go.sum, replace and workspace settings, then verify a clean build. Use when tidy produces churn, builds differ between machines or before tagging a module release.
author: Remedy Official
license: Apache-2.0
tags:
  - go
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - grep
metadata:
  source: library
  library_id: go-module-hygiene
  official: true
  security_flags: []
---

# Go Module Hygiene

## When to use
A Go module's dependency metadata needs to be trustworthy.

## Steps
1. Record `go version`, `go env GOFLAGS GOWORK GOPRIVATE GOPROXY GOTOOLCHAIN`, all `go.mod` and `go.work` files, and a clean `git status`.
2. Note the `go` and `toolchain` lines. Do not raise them without deciding the minimum version users need; a dependency update can raise them for you.
3. On versions that support it, preview with `go mod tidy -diff`; otherwise run tidy and review the diff. Explain every added, removed or upgraded requirement.
4. Check why a surprising module is present with `go mod why -m` and `go mod graph`.
5. Review each `replace`: local paths break clean checkouts, and replacements are ignored when another module depends on yours. Remove only after the upstream version builds.
6. Test as consumers will with `GOWORK=off`, since a workspace can hide a missing requirement.
7. Run `go mod verify`, `go build ./...`, `go vet ./...` and `go test ./...` per module. Cover relevant build tags and target OS builds; tidy considers most tags, a plain build does not.
8. Check retracted or deprecated modules with `go list -m -u -retracted all` and report them; upgrade as a separate change.
9. If vendoring, run `go mod vendor` and review it.

## Watch out for
- `go get -u` upgrades widely; it is not cleanup.
- Disabling checksum verification to silence a mismatch removes protection; find out why content changed.
- Private modules need `GOPRIVATE`, with credentials kept out of the repository.
- Root `./...` does not enter nested modules.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Tidy produces no further diff, each module builds and tests without unintended workspace help, and every dependency change is explained.
