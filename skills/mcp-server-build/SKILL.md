---
name: mcp-server-build
version: 1.0.0
description: >
  Build and test a Model Context Protocol server with a few task-shaped tools, safe inputs and the right transport. Use when exposing an API, database or local capability to AI clients.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - mcp
  - tools
kind: native
status: discovered
tools:
  - web.fetch
  - read
  - write
  - edit
  - bash
metadata:
  source: library
  library_id: mcp-server-build
  official: true
  domain: llm
  security_flags: []
---

# Mcp Server Build

## When to use
A service or local function should be callable by MCP-compatible clients.

## Steps
1. Read the current specification and official SDK documentation for the installed version, and check which revision the target clients speak; the protocol changes between revisions (2026-07-28, for example, removed the session handshake).
2. Choose transport: stdio for a local process launched by the client, Streamable HTTP for a networked service.
3. Design tools around user tasks, not one per endpoint. For each, set name, description of when to use it, input schema, output size limit and side effects. Use resources or prompts only if target clients support them.
4. Mark read-only and destructive behaviour with annotations, but enforce rules in the server; annotations are hints.
5. Validate every argument. Constrain paths after resolving links, parameterize queries, and pass command arguments as a list without a shell.
6. Return actionable tool errors as tool results flagged as errors; leave protocol errors for protocol faults.
7. On stdio, write only protocol messages to stdout and send logs to stderr.
8. For HTTP, follow the specification's authorization guidance, validate `Origin`, bind to localhost for local use, do not forward the client's token to upstream APIs, and scope data per authenticated user.
9. Load credentials from the environment or a secret store, never tool arguments or results.
10. Test with the MCP Inspector (`npx @modelcontextprotocol/inspector`; ask before it downloads) plus automated tests for bad input, timeout, large output and unauthorized access.
11. Connect a real client and try natural requests to see whether the model picks the right tool.

## Watch out for
- A stray `print` or library banner breaks stdio sessions.
- A generic "run any query" tool grants far more than the task needs.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A real client lists and calls each tool successfully, invalid input fails safely, and tests cover side-effecting tools.
