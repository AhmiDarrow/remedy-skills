---
name: artifact-promotion-pipeline
version: 1.0.0
description: >
  Restructure delivery so one built artifact is tested and promoted by digest from staging to production instead of rebuilt per environment. Use when each environment runs its own build.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - ci
  - release
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: artifact-promotion-pipeline
  official: true
  domain: ops
  security_flags: []
---

# Artifact Promotion Pipeline

## When to use
Staging passes but production runs a separately built binary or image, or nobody can say which commit is live.

## Steps
1. Trace how each environment gets its software today and list what differs between builds: arguments, env files, base image pulls, compile-time flags.
2. Move environment-specific values out of the build into runtime configuration. Front-end bundles often bake in API URLs; load them from a served config file or inject at start.
3. Build exactly once per commit on the main line. Tag with the commit SHA and record the registry digest as the build output.
4. Run tests and scans against that digest.
5. Promote by deploying the same digest. Human-friendly tags such as `staging` or a version number may point at it but are never what deployment manifests resolve.
6. Record per environment: digest, commit, who or what promoted it and when. A Git file per environment works and gives history.
7. Gate production on evidence attached to that digest, not on a branch name.
8. Set registry retention so any digest currently deployed, plus several previous releases, cannot be garbage collected.
9. Expose the commit SHA from the running service and compare it with the record after each deploy.

## Watch out for
- Rebuilding "the same commit" later can pull a newer base image or dependency and produce different software.
- Retention rules that delete untagged images can remove what is running; the failure appears only when a node reschedules.
- Copying between registries can change a digest if the tool converts the manifest. Use a copy that preserves it and compare afterwards.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Staging and production report the same digest for a release, and no production step invokes a build.
