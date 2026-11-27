---
name: tracing-spans
version: 1.0.1
description: >
  Add distributed tracing so one request can be followed across services, queues and database calls. Use when latency or errors cross service boundaries and logs cannot show where time goes.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - observability
kind: native
status: discovered
tools:
  - read
  - write
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: tracing-spans
  official: true
  security_flags: []
---

# Tracing Spans

## When to use
A request passes through several components. OpenTelemetry is the usual choice if the project has no tracing library; check the current documentation for the language.

## Steps
1. Find existing tracing, agents, exporters, propagation format and collector. Avoid installing a second system or instrumenting a library twice.
2. Pick one slow or failing journey and list every hop, including queues and background work.
3. Initialise the SDK once at process start, before libraries that need patching are loaded, with service name, version and environment.
4. Use maintained instrumentation for HTTP, RPC, database and messaging first. Add manual spans only around meaningful operations that it cannot see.
5. Keep span names low in cardinality, such as a route template; put ids in attributes only when allowed. Follow semantic conventions. Record errors and set error status on failed spans.
6. Propagate context with the configured standard, such as W3C `traceparent`, in HTTP headers and message metadata. Pass context explicitly where threads, callbacks or tasks lose it. For batches or fan-in, use span links.
7. Close spans on every path, including exceptions and cancellation. Streaming spans end when the stream does.
8. Exclude tokens, bodies, personal data and raw query values. Check what automatic instrumentation captures by default. Do not trust inbound context or baggage from outside without a policy, and do not send baggage to third parties.
9. Choose sampling: parent-based keeps decisions consistent; keeping all errors or slow traces needs tail sampling in a collector.
10. Export through a batching processor, flush on shutdown, and verify one success and one failure in the trace viewer.

## Watch out for
- Broken traces appearing as several unrelated roots after a queue or proxy.
- A span per loop item creating enormous traces.
- Exporter outages blocking requests or growing memory.
- Local tests at full sampling that hide what production will drop.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A test request appears as one connected trace across the intended hops with correct errors and no sensitive attributes, and sampling is documented.
