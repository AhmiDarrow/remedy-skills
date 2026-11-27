---
name: maven-dependency-conflict-fix
version: 1.0.0
description: >
  Resolve Maven classpath conflicts behind NoSuchMethodError and ClassNotFoundException. Use when code compiles but fails at runtime after adding or upgrading a dependency.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - java
  - maven
  - dependencies
kind: native
status: discovered
tools:
  - read
  - bash
  - edit
  - grep
metadata:
  source: library
  library_id: maven-dependency-conflict-fix
  official: true
  domain: tooling
  security_flags: []
---

# Maven Dependency Conflict Fix

## When to use
Linkage errors appear at runtime in a Maven build.
## Steps
1. Read the missing class or method signature from the error. That identifies the library to investigate.
2. Find which jars on the runtime classpath contain the class. Check for two artifacts providing the same package, including renamed coordinates and shaded copies.
3. Run `mvn dependency:tree -Dverbose -Dincludes=<groupId>:<artifactId>` to see every requested version and which were omitted.
4. Remember Maven picks the nearest declaration in the tree, then the first declared at equal depth. It does not pick the newest.
5. Determine the version that satisfies all users from their release notes; check whether the method exists with `javap` against the candidate jar.
6. Pin it in `dependencyManagement`, or import the framework's BOM and remove hand-set versions it manages.
7. Use `exclusions` only to remove duplicate coordinates or an unwanted transitive, with a comment.
8. Check scopes: `provided` and `test` dependencies differ between your tests and the deployed runtime. Inspect the packaged artifact's lib folder.
9. Add an enforcer rule such as dependency convergence or banned dependencies to stop recurrence.
10. Confirm effective settings with `mvn help:effective-pom` when a parent POM overrides you.
## Watch out for
- Application servers and containers may supply their own copy that wins over yours.
- IDE classpaths can differ from Maven's; reproduce with the command line and packaged artifact.
- Two incompatible major versions under the same package cannot both be satisfied; upgrade a consumer or relocate with shading.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The packaged application contains exactly one copy of the class at the chosen version, and the failing path runs.
