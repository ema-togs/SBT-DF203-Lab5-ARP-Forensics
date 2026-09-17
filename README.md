# SBT-DF203 Lab 5: Network Forensics - ARP Cache Poisoning

## Executive Summary
This repository contains the complete forensic investigation and laboratory artifacts for **SBT-DF203 Lab 5**. The analysis focuses on investigating dynamic Layer-2 address resolution behavior, detecting unsolicited ARP spoofing attempts, isolating attacker/victim hardware identities, executing host-level remediation, and defining enterprise prevention strategies.

---

## Repository Structure
```text
SBT-DF203-Lab5/
├── evidence/      # Original raw network evidence files (arp.pcap)
├── working/       # Analysis working copies and baseline captures
├── reports/       # Extracted logs, TSV files, and command execution outputs
├── scripts/       # Automation and field parsing scripts
├── exported/      # Reconstructed objects and extracted session artifacts
└── screenshots/   # Terminal evidence captures and execution verification
Forensic Analysis Summary
1. Baseline vs. Poisoned Capture Analysis
Normal Resolution: Baselined baseline ARP request (opcode 1) broadcast frames followed by legitimate unicast response (opcode 2) frames.

Malicious Activity: Isolated unsolicited unicast ARP replies exchanged directly between hosts 136.160.215.194 and 136.160.215.15 in working/arp_working.pcap.

2. Primary Evidence Verification
Evidence File: evidence/arp.pcap

SHA-256 Hash: 342a75dc002d090cc7fd108994b6c0c9c8eaa3962cf642159b4507d5615adc3e

3. Detection Rules & Logic
Unsolicited ARP Replies: Flagged opcode 2 frames lacking a corresponding recent broadcast query.

IP-to-MAC Spoofing: Isolated single MAC entities asserting ownership over multiple distinct IP identities (gateway and victim hosts).

Traffic Redirection: Correlated Layer-2 address re-bindings with intercepted HTTP/DNS traffic streams.

4. Remediation & Prevention
Host Cleanup: Executed sudo ip neigh flush all and verified clean neighbor table output alongside zero lingering background spoofing processes (ps aux | grep -E '[a]rp.py|[s]capy').

Enterprise Defenses: Enforced Dynamic ARP Inspection (DAI), DHCP Snooping, Port Security, Network Segmentation, and Encrypted Application Protocols (TLS/SSH).

Author
Investigator: ema-togs

Lab Identifier: SBT-DF203-Lab5
