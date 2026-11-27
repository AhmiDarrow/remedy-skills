---
name: prompt-injection-hardening
version: 1.0.0
description: >
  Limit what malicious text in documents, pages or messages can make a model-powered app do, using least privilege and tests. Use when a model reads untrusted content and can use data or tools.
author: Remedy Official
license: Apache-2.0
tags:
  - llm
  - agents
  - hardening
kind: native
status: discovered
tools:
  - read
  - grep
  - edit
  - bash
metadata:
  source: library
  library_id: prompt-injection-hardening
  official: true
  domain: llm
  security_flags: []
---

# Prompt Injection Hardening

## When to use
Your own application feeds outside content to a model that can also see private data or take actions.

## Steps
1. Map every untrusted input (web, email, files, tool results, retrieved chunks, memory, tool descriptions) and every sensitive read and side-effecting tool.
2. Find paths where one session has untrusted content, private data and a way to send data out. Remove at least one of the three.
3. Look for quiet exits: URLs in rendered images or links, web requests, DNS, shared documents.
4. Enforce authorization in code using the end user's identity. Tool arguments from the model never grant access.
5. Narrow tools: specific operations, allow-listed destinations, read-only by default.
6. Require confirmation for sending, deleting, paying or publishing, showing the actual recipient and content generated from the arguments, not the model's summary.
7. Consider separating roles: a tool-less step processes untrusted text and returns only validated fields to the privileged step.
8. Sanitize rendered output and block automatic loading of remote resources.
9. Mark where content came from, including through memory and summaries.
10. In a test environment with dummy data, plant harmless canary instructions in each input channel and assert on tool calls and outbound requests, not only reply text.

## Watch out for
- Delimiters, warnings in the system prompt and detection filters help but are not a security boundary.
- A few failed attacks do not prove safety; judge by what a fully hijacked model could do.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
For every input channel, the worst action a hijacked model could take is documented and acceptable, and canary tests cause no unauthorized call or data exit.
