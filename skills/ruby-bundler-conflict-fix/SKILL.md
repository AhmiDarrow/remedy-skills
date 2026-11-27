---
name: ruby-bundler-conflict-fix
version: 1.0.0
description: >
  Resolve Bundler version conflicts and native gem install errors in Ruby projects. Use when bundle install fails or the app activates the wrong gem version.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - ruby
  - dependencies
  - build
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
metadata:
  source: library
  library_id: ruby-bundler-conflict-fix
  official: true
  domain: tooling
  security_flags: []
---

# Ruby Bundler Conflict Fix

## When to use
Bundler cannot resolve, compile or activate gems.
## Steps
1. Confirm which Ruby and Bundler run: `ruby -v`, `which ruby`, `bundle -v`, `bundle env`. Compare with `.ruby-version`, the Gemfile `ruby` line and the `BUNDLED WITH` entry in `Gemfile.lock`.
2. Separate the failure type: resolution, native extension build, or activation at runtime.
3. For resolution, read the conflict explanation and use `bundle info` and `gem dependency` to find who constrains the shared gem.
4. Update conservatively: `bundle update --conservative <gem>`. To preview, use `bundle lock --update <gem> --print`; without `--print` it rewrites `Gemfile.lock` (check `bundle lock --help` on the installed version).
5. Check `bundle outdated <gem>` before loosening a pin, and read its changelog.
6. For native builds, open the `mkmf.log` path named in the error; it contains the real missing header or library. Pass build options with `bundle config build.<gem>` after installing the system package, with approval.
7. For deploy platforms missing from the lock, add them with `bundle lock --add-platform <platform>`.
8. For activation errors, run commands through `bundle exec` or the project's binstubs.
9. Verify with a clean install into a separate path, then run tests.
## Watch out for
- `bundle update` with no gem name upgrades the entire lock.
- Deleting `Gemfile.lock` loses the known-good set.
- Using sudo to install gems mixes system and project gems and causes later permission trouble.
- Git-sourced gems pinned to a branch can change under you; pin a ref.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A clean `bundle install` succeeds with the committed lock on development and deploy platforms, and tests run via `bundle exec`.
