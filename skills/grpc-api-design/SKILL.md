---
name: grpc-api-design
version: 1.0.1
description: >
  Design or review gRPC and Protocol Buffers services for wire compatibility, deadlines, status codes and safe retries. Use when writing or changing .proto files or debugging cross-service calls.
author: Remedy Official
license: Apache-2.0
tags:
  - api
  - grpc
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
  library_id: grpc-api-design
  official: true
  security_flags: []
---

# Grpc Api Design

## When to use
A service contract in `.proto` files is being created or changed.

## Steps
1. Read existing protos, package layout, generation config and style so the new contract matches.
2. Give each RPC its own request and response message, even when nearly empty, so either can grow.
3. Protect compatibility: never change or reuse a field number; when deleting, add both number and name to `reserved`. Renaming keeps binary wire format but breaks generated code and JSON.
4. Model presence deliberately. In proto3 a plain scalar cannot distinguish unset from zero; use `optional` or a wrapper, and a field mask for partial updates. Start enums with an `_UNSPECIFIED` zero value and handle unknown values.
5. Choose canonical status codes: `INVALID_ARGUMENT`, `NOT_FOUND`, `ALREADY_EXISTS`, `PERMISSION_DENIED`, `UNAUTHENTICATED`, `FAILED_PRECONDITION`, `ABORTED` for concurrency conflicts, `UNAVAILABLE` for retryable outage. Put structured details in the supported error model.
6. Require callers to set deadlines, propagate them downstream, and stop work on cancellation.
7. State which methods are safe to retry. Give creating or charging calls a request id the server deduplicates.
8. Paginate lists with page size and opaque token; keep unary messages small and stream large transfers, defining how a broken stream resumes.
9. Run the project's lint and breaking-change check (for example `buf lint` and `buf breaking` if configured), generate code and build consumers.

## Watch out for
- `DEADLINE_EXCEEDED` does not prove the server did nothing.
- Changing a field's type is safe only for a few documented pairs; assume unsafe otherwise.
- Long-lived HTTP/2 connections can pin all traffic to one backend behind a connection-level load balancer.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Lint and compatibility checks pass or are reported unavailable, generated consumers build, and each RPC has stated deadline, error and retry behaviour.
