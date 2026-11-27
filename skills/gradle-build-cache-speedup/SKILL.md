---
name: gradle-build-cache-speedup
version: 1.0.0
description: >
  Speed up Gradle builds with configuration cache, build cache and correct task inputs. Use when Gradle reruns tasks with no changes or spends long in configuration.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - gradle
  - build
  - performance
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - grep
metadata:
  source: library
  library_id: gradle-build-cache-speedup
  official: true
  domain: tooling
  security_flags: []
---

# Gradle Build Cache Speedup

## When to use
A Gradle project is slow locally or in CI.
## Steps
1. Use the wrapper (`./gradlew` or `gradlew.bat`) and record its version.
2. Measure with `--profile` or a build scan if the team permits uploading build data. Separate configuration time, dependency resolution and task execution.
3. Run the same build twice. Anything not UP-TO-DATE or FROM-CACHE on the second run is a defect; find the reason with `--info`.
4. Enable `org.gradle.caching=true` and `org.gradle.parallel=true`, measuring each.
5. Try `--configuration-cache`, read its problem report, and fix scripts that read project state or the environment at execution or configuration time in unsupported ways.
6. Replace eager task APIs with lazy ones (`tasks.register`, `configureEach`) and move network calls and shell commands out of configuration.
7. For custom tasks, declare every input and output, set path sensitivity to relative where location does not matter, and mark cacheable only when outputs are deterministic.
8. Find volatile inputs such as timestamps, absolute paths or git hashes written into resources on every build.
9. Check daemon memory in `gradle.properties` and look for repeated daemon restarts from differing JVM arguments or JDKs.
## Watch out for
- `clean` before every build throws away the incremental benefit and often hides an undeclared input.
- A shared remote cache should be writable only by trusted CI, or a bad artifact spreads to everyone.
- Dynamic versions such as `1.+` make resolution slow and builds unrepeatable.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A no-change second build executes no unnecessary tasks, and timings for the same command before and after are recorded.
