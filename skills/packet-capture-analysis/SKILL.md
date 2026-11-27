---
name: packet-capture-analysis
version: 1.0.0
description: >
  Capture and read network traffic on systems you administer to prove where a connection fails. Use when logs on both ends disagree about what was sent or received.
author: Remedy Official
license: Apache-2.0
tags:
  - ops
  - networking
  - debugging
kind: native
status: discovered
tools:
  - bash
  - read
metadata:
  source: library
  library_id: packet-capture-analysis
  official: true
  domain: ops
  security_flags: []
---

# Packet Capture Analysis

## When to use
Timeouts, resets or protocol oddities that application logs cannot explain. Capture only on networks and hosts you are authorised to monitor.

## Steps
1. Write the question first, for example "does the SYN reach the server?"
2. Choose capture points, ideally both ends at once with synchronised clocks.
3. Filter narrowly and write to a file: `tcpdump -i <iface> -nn -s 0 -w case.pcap host <ip> and port <port>`. Bound it with rotation or a packet count. On Windows, `pktmon` or Wireshark can capture.
4. Reproduce once and stop.
5. Classify the TCP pattern. Repeated SYN with no reply: drop or routing. RST in reply to SYN: nothing listening or an active reject. Handshake then stall on large packets: suspect MTU. Data retransmitted: loss on the path or return path. Zero window: the receiver is not reading.
6. Note who sends FIN or RST first and the idle time before it, which exposes NAT and firewall timeouts.
7. In Wireshark use filters such as `tcp.flags.reset==1` and `tcp.analysis.retransmission`.
8. For TLS, read the ClientHello server name, negotiated version and alerts without decrypting.
9. Compare the two captures to find the hop where packets vanish or change.

## Watch out for
- Captures on the sending host may show wrong checksums and oversized segments because of hardware offload; that is usually not the fault.
- Port filters can miss the ICMP messages that explain the failure.
- Traffic may use another interface or loopback.
- Capture files contain credentials, cookies and personal data. Restrict them, do not upload them to online analysers, and delete after use.

## Operating rules
- Look before you change anything: read the real files, data or page first.
- Report what you actually ran and saw; never invent results, sources or numbers.
- Ask before destructive, paid, public or irreversible actions.
- Never print, store or commit secrets or private personal data.

## Done when
The question is answered with specific packets and timestamps, and capture files are deleted or stored under an agreed retention.
