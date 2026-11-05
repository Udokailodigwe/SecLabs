# Lab 03 — Windows Server and Active Directory

Domain `udokaudodigwe.com` on Hyper-V. DC01 is the domain controller. WKSTN01 is the member workstation.

| | |
| --- | --- |
| Date | 22–24 Jul 2026 |
| Host | Hyper-V on `UDOPC` |
| DC | `DC01`, Windows Server 2025 Standard Evaluation (`10.0.26100`) |
| Workstation | `WKSTN01`, Windows 11 (`10.0.26200`) |
| Domain | `udokaudodigwe.com` |

## Result

- DC01 is a domain controller with AD DS, DNS, DHCP, and WDS.
- Private NIC `172.16.0.1/16`. DHCP scope `172.16.0.100`–`172.16.0.200`, 8-day lease.
- WKSTN01 joined the domain from the external network (`10.0.0.134`, DNS `10.0.0.132`) and sits in the Marketing OU.
- Marketing Lockdown blocks Control Panel. Domain password policy is 10 characters, complexity on, 24 remembered, 30-day maximum age.
- `UdokaShare` grants `udoka.udodigwe` full share and NTFS control. WinRM from DC01 to WKSTN01 works.

## Contents

| Path | What it is |
| --- | --- |
| [docs/project.md](docs/project.md) | Build order, screenshots, and results |
| [evidence](evidence) | Screenshots by step, plus DC01 and WKSTN01 exports |
