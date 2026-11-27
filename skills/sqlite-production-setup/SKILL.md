---
name: sqlite-production-setup
version: 1.0.0
description: >
  Configure SQLite for an application with WAL mode, busy timeouts, enforced foreign keys and consistent backups. Use when shipping SQLite in a server or desktop app, or fixing database is locked errors.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - database
  - sqlite
kind: native
status: discovered
tools:
  - read
  - edit
  - grep
  - bash
metadata:
  source: library
  library_id: sqlite-production-setup
  official: true
  domain: backend
  security_flags: []
---

# Sqlite Production Setup

## When to use
SQLite is the real datastore of an app and needs to behave under concurrent use and survive crashes.

## Steps
1. Check the library version the app actually loads (`select sqlite_version();`), which can differ from the `sqlite3` command line tool.
2. Confirm the file is on a local disk. Network filesystems break SQLite locking, and WAL requires all processes on the same host.
3. Set `PRAGMA journal_mode=WAL;` once (it persists) and verify the returned value.
4. On every connection set `PRAGMA foreign_keys=ON;` and `PRAGMA busy_timeout` to a few seconds.
5. Choose `synchronous`: `FULL` keeps recent commits through power loss; `NORMAL` in WAL is faster and stays consistent but can lose the latest transactions.
6. Remember there is one writer at a time. Keep write transactions short, and start those that will write with `BEGIN IMMEDIATE`; upgrading a read transaction can fail with busy immediately, regardless of the timeout.
7. Use `STRICT` tables (3.37 and later) if type enforcement matters.
8. Version the schema with `PRAGMA user_version` or the project's migration tool. For table rebuilds follow the order in the SQLite ALTER TABLE documentation.
9. Back up with the backup API, `.backup` or `VACUUM INTO`, then open the copy and run `PRAGMA integrity_check;`.
10. Run `PRAGMA foreign_key_check;` before first enforcing foreign keys on existing data.

## Watch out for
- Copying only the `.db` file while the app runs can miss data still in the `-wal` file.
- A long-lived read transaction stops checkpoints from completing, so the WAL grows without bound.
- Connection libraries may open transactions implicitly; check the driver's behaviour.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
A concurrent read and write test runs without lock errors, pragmas are verified on a live app connection, and a backup restores and passes the integrity check.
