---
name: browser-automation-safe
version: 1.0.1
description: >
  Write or repair automated browser tests with user-facing selectors, condition-based waits, isolated data and failure traces. Use when scripting a UI flow or when browser tests are brittle.
author: Remedy Official
license: Apache-2.0
tags:
  - browser
  - e2e
  - testing
kind: native
status: discovered
tools:
  - bash
  - read
  - write
  - edit
  - grep
metadata:
  source: library
  library_id: browser-automation-safe
  official: true
  security_flags: []
---

# Browser Automation Safe

## When to use
You are writing browser test code. Run it against local or test environments; any action on production needs explicit approval.

## Steps
1. Use the project's existing runner, config and helpers. Confirm the target address and account are test ones before running.
2. Select as a user would: role with accessible name, label or visible text. Add a dedicated test ID where text is unstable. Avoid generated class names and positional chains.
3. Wait for the outcome, not for time. Use the runner's retrying assertions on visible state, URL or a specific response, and start listening for a response before the click that triggers it.
4. Make each test independent: create its own uniquely named data through an API or seed, and clean up. It must pass alone, repeated and in parallel.
5. Log in once through supported setup and reuse saved session state where the runner allows. That file contains live cookies, so ignore it in Git. Credentials come from the environment.
6. Stub third parties such as payment or email at the network edge, and say which flows that leaves unverified.
7. Assert the user-visible result and, for important writes, the stored result.
8. Keep trace, screenshot and console logs on failure. Run the new test repeatedly (for example Playwright's `--repeat-each`) before trusting it.

## Watch out for
- Forced clicks hide overlays or disabled controls a real user would hit.
- Waiting for network idle is unreliable on pages that poll.
- Blanket retries turn a real race into an occasional pass.
- Traces and videos can contain tokens and data; restrict artifact access.
- Never automate around CAPTCHAs or bot checks; use a test-environment setting the owner provides.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The flow passes repeatedly with no fixed sleeps, fails when the behaviour is deliberately broken, and leaves a usable artifact on failure.
