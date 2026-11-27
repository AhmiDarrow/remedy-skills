---
name: python-logging-config-repair
version: 1.0.0
description: >
  Fix Python logging that duplicates lines, drops messages or loses tracebacks. Use when logs appear twice, debug output never shows, or a library hijacks your handlers.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - python
  - logging
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
  library_id: python-logging-config-repair
  official: true
  domain: backend
  security_flags: []
---

# Python Logging Config Repair

## When to use
The program uses the standard `logging` module and its output does not match what the code seems to ask for.
## Steps
1. Dump the real tree at runtime: for the root and each suspect logger print `level`, `getEffectiveLevel()`, `handlers`, `propagate` and `disabled`.
2. Duplicates: look for a handler on both a child and an ancestor, or setup code that runs more than once (reloaders, notebook cells, per-request init). Configure handlers once, at the application entry point.
3. Missing messages: check both filters. The logger level and the handler level must each allow the record.
4. `grep` for `basicConfig`. It does nothing if the root already has handlers; pass `force=True` (3.8+) only in the entry point.
5. If loggers go silent after configuration, set `disable_existing_loggers` to false in `dictConfig`; its default disables loggers created earlier.
6. In libraries, use `logger = logging.getLogger(__name__)`, add at most a `NullHandler`, and set no levels on the root.
7. Replace `logger.error(str(e))` inside except blocks with `logger.exception(...)` or `exc_info=True` so the traceback survives.
8. Pass arguments lazily (`logger.debug("id=%s", x)`) and verify the format string and argument count match, since a mismatch only prints a logging error at emit time.
## Watch out for
- Multiple processes writing to one rotating file handler corrupt or lose logs; send records through a queue or log to stdout and rotate outside.
- Network or slow file handlers block the caller, including an event loop. Use `QueueHandler` with `QueueListener`.
- Changing the root level to DEBUG floods output from dependencies; set levels on your package logger.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
One test message at each level appears exactly as often and where intended, and a forced exception shows its full traceback.
