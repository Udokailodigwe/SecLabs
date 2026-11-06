# Lab 04 — Nmap and Wireshark scan patterns

Port discovery on a Windows Server, then a packet-level comparison of a full TCP connection and a half-open SYN scan.

| | |
| --- | --- |
| Date | 5 Nov 2026, 23:34–23:56 (UTC−5) |
| Scanner | Kali Linux on Hyper-V (`kaliUD`), user `udoka` |
| Target | Windows Server at `10.0.0.161`, IIS, Hyper-V MAC `00:15:5D:00:9F:14` |
| Tools | Nmap 7.99, Wireshark on `eth0`, Firefox |

## Result

- `nmap -p 1-65535` found 22 open ports. 65,513 ports were filtered. Firefox confirmed IIS on port 80.
- `-sS` leaves the handshake unfinished: SYN, SYN-ACK, RST.
- A full connection completes it: SYN, SYN-ACK, ACK, then RST.
- Ordinary browsing in the same capture is an HTTP GET, `200 OK`, and a FIN close.

## Contents

| Path | What it is |
| --- | --- |
| [docs/scan-patterns.md](docs/scan-patterns.md) | Captures in order |
| [evidence](evidence) | Four screenshots |
