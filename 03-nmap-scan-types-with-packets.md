# Nmap Scan Types, Explained With Packets

## Why this matters
Nmap's -sS and -sT both report the same open ports, but they behave very differently on the wire — which matters for stealth, privileges required, and what shows up in a target's logs.

## SYN scan (-sS) — the "half-open" scan
Command: sudo nmap -sS -p 21,22,80 10.0.2.3

Packet pattern per open port:
1. Kali → Target: SYN
2. Target → Kali: SYN, ACK
3. Kali → Target: RST   (connection never completes)

Needs root because it crafts raw SYN/RST packets directly rather than using the OS's normal socket API.

## Connect scan (-sT) — the "full handshake" scan
Command: nmap -sT -p 21,22,80 10.0.2.3

Packet pattern per open port:
1. Kali → Target: SYN
2. Target → Kali: SYN, ACK
3. Kali → Target: ACK   (handshake completes, connection is real)
4. Kali → Target: RST, ACK  (connection torn down)

Uses a normal OS socket connect — no special privileges needed, same mechanism as a Python port scanner using connect_ex().

## Takeaway
-sS is faster and quieter (fewer packets, connection never fully opens, less likely to be logged as a completed connection). -sT is slower and noisier but needs no elevated privileges. On a real engagement, a pentester would default to -sS when they have root, specifically to reduce the footprint on target logs.

## Evidence
Both captures (syn_scan.pcapng and connect_scan.pcapng) taken in my isolated Kali/Metasploitable lab, filtered on the target IP.
