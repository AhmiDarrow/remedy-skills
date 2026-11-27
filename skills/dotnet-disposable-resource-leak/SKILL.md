---
name: dotnet-disposable-resource-leak
version: 1.0.0
description: >
  Find and fix .NET leaks from undisposed objects, event subscriptions and misused HttpClient or DI lifetimes. Use when memory, handles or sockets grow in a C# process.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - csharp
  - dotnet
  - debugging
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: dotnet-disposable-resource-leak
  official: true
  domain: backend
  security_flags: []
---

# Dotnet Disposable Resource Leak

## When to use
A .NET process's memory, handle count or connection count rises with use.
## Steps
1. Decide what is growing: managed heap, native memory, handles or sockets. Watch with `dotnet-counters` and the OS process tools.
2. For managed growth, take two dumps or `dotnet-gcdump collect` snapshots apart in time and compare type counts. Both can pause the process (a gcdump forces a full collection), so get approval on production; full dumps hold secrets and user data and must stay private.
3. Use `dumpheap -stat` and `gcroot <address>` to find what keeps instances alive. Static collections, caches without limits and event handlers are the usual roots.
4. For events, unsubscribe in `Dispose` when the publisher outlives the subscriber.
5. Turn on analyzer rule CA2000 and related ones, then add `using` or `await using` where the code owns the object. Types implementing `IAsyncDisposable` should be disposed asynchronously.
6. Check HTTP usage: creating a new `HttpClient` per request can exhaust ports. Use `IHttpClientFactory` or a long-lived client with `PooledConnectionLifetime` set so DNS changes apply.
7. Check DI lifetimes: disposable transients resolved from the root provider are held until shutdown, and a scoped service captured by a singleton lives forever. Enable scope validation.
8. Dispose `CancellationTokenSource` instances, especially linked ones, and registrations on long-lived tokens.
9. Re-run the same repeated operation and compare snapshots.
## Watch out for
- Do not dispose objects you did not create, such as injected services.
- A high managed heap alone is not a leak; look for monotonic growth after collections.
- Adding finalizers to your classes delays reclamation; use safe handles for native resources.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
After many repetitions the instance and handle counts stay level, and the root that held the leaked objects is named.
