---
name: owasp-web-checklist
version: 1.0.1
description: >
  Security-review a web change by tracing untrusted input to injection, XSS, access control, CSRF, SSRF and error-handling risks. Use when reviewing a web pull request or endpoint for common vulnerabilities.
author: Remedy Official
license: Apache-2.0
tags:
  - security
  - web
kind: native
status: discovered
tools:
  - read
  - grep
  - glob
  - bash
metadata:
  source: library
  library_id: owasp-web-checklist
  official: true
  security_flags: []
---

# Owasp Web Checklist

## When to use
A diff or feature touches requests, rendering, data access or outbound calls. This is a focused code review, not a full penetration test; test live systems only with authorisation.

## Steps
1. Read the diff and list its inputs (parameters, body, headers, cookies, files, stored data, third-party responses) and its sinks.
2. Access control first: for each action, find the server check for this user on this object. Try changed IDs, other roles, and extra fields that bind to protected attributes.
3. Injection: parameterised queries; identifiers and sort fields from an allowlist; argument arrays without a shell for processes; no user input in templates compiled as code or in unsafe deserialisers.
4. XSS: find raw HTML sinks (`innerHTML`, `dangerouslySetInnerHTML`, `v-html`, template safe filters), user-controlled link URLs that allow `javascript:`, and data embedded in script blocks.
5. CSRF for cookie-authenticated changes: framework token or strict origin check; SameSite as extra defence; no state change on GET. Check session cookies are Secure and HttpOnly, and credentialed CORS does not reflect any origin.
6. SSRF: for server fetches of user-influenced URLs, allowlist destinations. Otherwise block private, loopback and link-local addresses after DNS resolution, on every redirect, and connect to the checked address.
7. Check redirects, path joins, file uploads, rate limits on guessable actions, secrets in code, and errors or logs that expose stack traces or tokens.
8. For each finding give file and line, attacker, input, effect, severity and fix. Confirm with a safe local test where possible and label the rest unconfirmed.

## Watch out for
- A pattern match is not a finding until untrusted data reaches the sink.
- Client-side validation and hidden buttons protect nothing.
- Code outside the diff, such as shared middleware, may be what makes it safe or unsafe; read it.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
Every changed input path has been checked against the relevant categories, and the report lists confirmed findings, unconfirmed concerns and what was not reviewed.
