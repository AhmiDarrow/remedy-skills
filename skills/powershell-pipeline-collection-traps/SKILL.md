---
name: powershell-pipeline-collection-traps
version: 1.0.0
description: >
  Fix PowerShell bugs from pipeline output, single-item unrolling and accidental return values. Use when a function returns extra objects or Count and indexing behave strangely.
author: Remedy Official
license: Apache-2.0
tags:
  - tooling
  - powershell
  - debugging
kind: native
status: discovered
tools:
  - read
  - edit
  - bash
metadata:
  source: library
  library_id: powershell-pipeline-collection-traps
  official: true
  domain: tooling
  security_flags: []
---

# Powershell Pipeline Collection Traps

## When to use
Results have the wrong type or shape although each line looks right.
## Steps
1. Inspect the actual value with `$x.GetType().FullName` and `Get-Member -InputObject $x`; piping into `Get-Member` shows element types instead.
2. In misbehaving functions, find every expression whose result is not assigned. All of it becomes output, not only what follows `return`. Discard with `$null = ...` or `[void]`, for example on `ArrayList.Add`.
3. Where callers expect a list, wrap the call in `@( )` so zero or one result still behaves as an array.
4. To return an array as one object, use the unary comma `return ,$array`, and then do not also wrap the call in `@( )`.
5. Put `$null` on the left in comparisons (`$null -eq $x`); with a collection on the left, operators filter instead of returning a boolean.
6. Do not build large arrays with `+=` in loops, which copies each time; assign the loop output to a variable or use a generic list.
7. Check `process` blocks: a pipeline function without one handles only the last item.
8. Remember `ForEach-Object` and `foreach` differ: `return` in the script block moves to the next item, and `break` can end more than you expect.
9. Add tests for zero, one and many items.
## Watch out for
- A hashtable passes through the pipeline as a single object; use `GetEnumerator()` to iterate entries.
- `Format-Table` inside a function returns formatting objects, destroying the data for callers.
- Property access on a collection returns member values from all items, which can hide that you had many.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The function's output type and count are correct for zero, one and many inputs.
