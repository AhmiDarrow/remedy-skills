---
name: java-gc-pause-diagnosis
version: 1.0.0
description: >
  Diagnose JVM latency spikes and memory pressure from garbage collection logs. Use when a Java or Kotlin service pauses, spends high CPU in GC or throws OutOfMemoryError.
author: Remedy Official
license: Apache-2.0
tags:
  - backend
  - java
  - jvm
  - performance
kind: native
status: discovered
tools:
  - read
  - bash
  - grep
  - edit
metadata:
  source: library
  library_id: java-gc-pause-diagnosis
  official: true
  domain: backend
  security_flags: []
---

# Java Gc Pause Diagnosis

## When to use
Latency outliers or memory failures in a JVM service.
## Steps
1. Record the version and effective flags: `java -version` and `jcmd <pid> VM.flags`. Note container memory limits and the collector actually selected.
2. Enable unified GC logging on JDK 9+, for example `-Xlog:gc*,safepoint:file=gc.log:time,uptime:filecount=5,filesize=20m`.
3. Correlate pause timestamps with the latency spikes. If they do not line up, check safepoint times, CPU throttling and swapping before tuning GC.
4. Track heap occupancy after each full or old-generation cycle. A rising floor means retention or a leak; a flat floor with frequent young collections means high allocation rate.
5. For retention, take a heap dump (`jcmd <pid> GC.heap_dump <path>`) and follow dominator paths in a heap analyzer. Warn first: it pauses the JVM and the file contains live data, including secrets.
6. For allocation, record with Java Flight Recorder (`jcmd <pid> JFR.start duration=120s filename=a.jfr`) and inspect allocation sites. Treat recordings as sensitive too: they can include system properties, environment variables and command lines.
7. Read the OOM message: heap space, Metaspace, direct buffer memory, and "unable to create native thread" have different causes and fixes. A kernel OOM kill leaves no Java message.
8. Change one thing at a time: fix the retention or allocation first, then heap size (`-Xmx` or `-XX:MaxRAMPercentage`), then collector or pause target.
## Watch out for
- Giving the heap the entire container limit leaves no room for metaspace, threads and off-heap buffers.
- Flag lists copied from old articles may be removed or harmful on the installed JDK.
- Calling `System.gc()` hides symptoms and adds full pauses.
## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
GC logs from comparable load show the pause or footprint problem reduced, and the cause is identified from log, dump or recording evidence.
