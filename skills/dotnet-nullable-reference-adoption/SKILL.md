---
name: dotnet-nullable-reference-adoption
version: 1.0.0
description: >
  Adopt C# nullable reference types in an existing codebase without drowning in warnings. Use when enabling Nullable in a legacy project or cleaning up scattered null-forgiving operators.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - csharp
  - dotnet
  - refactoring
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
  - todo
metadata:
  source: library
  library_id: dotnet-nullable-reference-adoption
  official: true
  domain: tooling
  security_flags: []
---

# Dotnet Nullable Reference Adoption

## When to use
Null reference exceptions recur and the project does not yet have nullable annotations enabled.
## Steps
1. Count the damage by building once with `<Nullable>enable</Nullable>` locally, then revert.
2. Roll out with per-file `#nullable enable`, starting with leaf libraries and domain models that others depend on. `<Nullable>warnings</Nullable>` can surface likely dereferences first, but it leaves annotations off, so enable them in a file before adding `?`.
3. In each file annotate honest contracts first: which parameters, returns and properties can really be null. Check callers and data sources before deciding.
4. For data objects populated by serializers or an ORM, use `required` (C# 11+) or constructors where the framework supports it, and make genuinely optional columns nullable.
5. At trust boundaries keep runtime checks such as `ArgumentNullException.ThrowIfNull`; annotations are not enforced at runtime.
6. Describe helper behavior with attributes like `NotNullWhen` and `MemberNotNull` so callers need no overrides.
7. Treat each `!` as debt: allow it only with a comment saying why the compiler cannot know.
8. When a file is clean, promote warnings to errors for it, using `WarningsAsErrors` with `nullable` once the project is done.
9. Run tests after each project; changing a return to handle null can alter behavior.
## Watch out for
- Marking everything `?` silences the source and floods callers.
- `default!` on a property claims non-null while it holds null.
- Public library annotation changes are visible to consumers and can add warnings to their builds.
- JSON deserializers may assign null to a non-nullable property unless configured or validated.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The chosen projects build with nullable warnings as errors, and each remaining null-forgiving operator has a stated reason.
