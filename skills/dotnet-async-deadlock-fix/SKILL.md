---
name: dotnet-async-deadlock-fix
version: 1.0.0
description: >
  Fix .NET async deadlocks and thread pool starvation caused by blocking on tasks and misused async patterns. Use when a C# app hangs or request latency collapses under load.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - csharp
  - dotnet
  - concurrency
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: dotnet-async-deadlock-fix
  official: true
  domain: backend
  security_flags: []
---

# Dotnet Async Deadlock Fix

## When to use
Threads wait on tasks that need those same threads or that synchronization context.
## Steps
1. `grep` for `.Result`, `.Wait()`, `GetAwaiter().GetResult()` and `Task.WaitAll`.
2. Identify the host. UI apps and classic ASP.NET have a synchronization context, so blocking can deadlock outright. ASP.NET Core and console apps have none, and the symptom is starvation instead.
3. For starvation, run `dotnet-counters monitor --process-id <pid>` and watch thread pool queue length and thread count climbing while CPU stays modest.
4. Capture stacks with `dotnet-stack report` or a dump from `dotnet-dump collect`, then use `clrstack -all` and `dumpasync` in analysis. Dumps hold sensitive memory.
5. Make the chain async from the entry point down; do not wrap a blocking call in `Task.Run` just to hide it.
6. Replace `async void` with `async Task`, except true event handlers, which need a try/catch around the whole body.
7. In general-purpose libraries use `ConfigureAwait(false)`; application code in UI handlers usually needs the context.
8. Replace `lock` around awaited work with `SemaphoreSlim.WaitAsync` and release in `finally`.
9. Pass `CancellationToken` through and set timeouts on outbound calls.
10. Load test at the concurrency that triggered the hang.
## Watch out for
- Raising the minimum thread count hides starvation and returns at higher load.
- Constructors and property getters cannot be async; use an async factory method.
- `Task.WhenAll` surfaces only the first exception on await; inspect the tasks for the rest.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The load test completes without queue growth or hangs, and no sync-over-async remains on the affected path.
