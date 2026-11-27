---
name: rust-clippy-fix
version: 1.0.1
description: >
  Run Clippy across a Cargo workspace and resolve warnings safely, handling features, MSRV and automatic fixes. Use when Clippy fails in CI or a crate needs a lint cleanup.
author: Remedy Official
license: Apache-2.0
tags:
  - rust
  - quality
kind: native
status: discovered
tools:
  - bash
  - read
  - edit
  - grep
metadata:
  source: library
  library_id: rust-clippy-fix
  official: true
  security_flags: []
---

# Rust Clippy Fix

## When to use
Rust lints must pass without changing behaviour by accident.

## Steps
1. Reproduce the CI command, toolchain and `RUSTFLAGS`. Read `rust-toolchain.toml`, `rust-version`, `clippy.toml` and any `[lints]` tables.
2. With no CI command, start with `cargo clippy --workspace --all-targets -- -D warnings`. Check meaningful feature sets separately; `--all-features` fails or misleads when features are exclusive. Platform-gated code needs its target.
3. Group by lint. Handle correctness and suspicious findings first, then performance and complexity, then style. `cargo clippy --explain <lint>` describes one.
4. Run `cargo test` for a baseline.
5. Apply `--fix` only from a clean, committed tree, then read the whole diff. Avoid forcing it onto a dirty tree.
6. Check behaviour-sensitive rewrites: eager against lazy evaluation, drop order and lock guard lifetimes, integer casts and overflow, public signature changes and newer APIs beyond the minimum Rust version.
7. For a justified exception, use the narrowest `allow` (or `expect` where the MSRV supports it) with a reason.
8. Rerun lints for each feature set, tests, and formatting only as the project practises it.

## Watch out for
- A newer toolchain adds lints; do not mix a toolchain upgrade into unrelated work unnoticed.
- Enabling all pedantic or restriction lints produces conflicting advice.
- Fixing needless pass-by-value in a public API breaks callers.
- Some formatted repositories are hand-formatted; do not reformat the tree.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The agreed Clippy commands pass, tests pass, and every new suppression has a reason and the smallest scope.
