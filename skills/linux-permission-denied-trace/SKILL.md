---
name: linux-permission-denied-trace
version: 1.0.0
description: >
  Trace a Linux permission denied error through path modes, ACLs, mount options, attributes, SELinux or AppArmor and sandboxing. Use when access fails although the file permissions look right.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - linux
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: linux-permission-denied-trace
  official: true
  domain: ops
  security_flags: []
---

# Linux Permission Denied Trace

## When to use
A user or service cannot read, write, execute or bind, and `ls -l` does not explain it.

## Steps
1. Capture the exact operation, path and the real identity of the failing process (`ps -o user,group,supgrp`, or `/proc/<pid>/status`). `strace -f -e trace=%file` can reveal the actual path and error.
2. Walk every component with `namei -l <path>`; each parent directory needs execute (search) permission.
3. Remember deleting or renaming depends on the parent directory's write bit and sticky bit, not the file's mode.
4. Check ACLs with `getfacl`, including the mask.
5. Check attributes with `lsattr`; immutable and append-only override mode bits.
6. Check mount options with `findmnt -T <path>` for `ro`, `noexec` or `nosuid`, and NFS identity mapping.
7. For SELinux, check `getenforce`, `ls -Z` and `ausearch -m avc -ts recent`; fix with the right context (`semanage fcontext` then `restorecon`) or boolean. For AppArmor, search kernel logs for DENIED.
8. Check service sandboxing such as `ProtectSystem` or `ReadWritePaths`, and container user namespaces and volume labels.
9. For ports below the unprivileged threshold, grant the specific capability or use socket activation.
10. Test the smallest change as the failing identity.

## Watch out for
- `chmod -R 777` and running as root hide the cause and open the system.
- New group membership applies only to new sessions or restarted services.
- Turning SELinux off is not a fix; permissive mode for diagnosis needs approval and must be restored.
- `sudo echo x > file` performs the redirect as your own user.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The denying layer is identified with evidence and the operation succeeds with the narrowest change, with security modules still enforcing.
