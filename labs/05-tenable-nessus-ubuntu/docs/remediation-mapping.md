# Vulnerability assessment — remediation mapping

I correlated my original [VA report](../reports/va-remediation-report.docx) with the Nessus summaries. The report's own severity numbers are retained below as report ratings, not scanner CVSS scores. Nessus marks informational findings CVSS N/A. Actions are report recommendations or reported actions, not verified remediation.

## Kali Linux — 10.0.0.145

| Nessus plugin / finding | Report rating | Remediation in my report |
| --- | ---: | --- |
| 10114 — ICMP timestamp disclosure (Medium, CVSS 4.0) | 4.0 | Block ICMP types 13 and 14 using host firewall rules. |
| 35716 — Ethernet card manufacturer | 3.5 / 2.5 | Restrict discovery and untrusted network access; no direct fix required. Two report entries describe the same finding. |
| 86420 — Ethernet MAC addresses | 3.1 | Limit network access to trusted systems. |
| 84047 — Hyper-V VM detection | 3.1 | Patch Hyper-V host and restrict management access. |
| 10287 — Traceroute information | 3.0 | Restrict unnecessary ICMP type 11 at the boundary after assessing operational impact. |
| 19506 — Nessus scan information | — | No specific remediation in report; scanner metadata. |

## Windows 11 host — 10.0.0.159

| Nessus plugin / finding (Info) | Report rating | Remediation in my report |
| --- | ---: | --- |
| 10736 — DCE services enumeration | 3.1 | Restrict TCP 135 and dynamic RPC ports to trusted management IPs. |
| 10785 — SMB NativeLanManager information disclosure | 3.5 | Restrict inbound TCP 445 to authorized clients; disable SMB if unnecessary. |
| 11011 — SMB service detection | 3.5 | Block TCP 445 from untrusted networks. |
| 11219 — Nessus SYN scanner | 3.5 | Review open ports and disable unnecessary services; scanner discovery is not itself a vulnerability. |
| 10150 — NetBIOS/SMB host information disclosure | 3.8 | Restrict SMB/NetBIOS access and disable unnecessary NetBIOS services. |
| 43815 — NetBIOS multiple IP address enumeration | 3.8 (related) | Same NetBIOS restriction is relevant; no separate report entry. |
| 100871 — SMB versions supported | — | No explicit version-specific remediation in report; review supported versions as a next step. |

## Windows Server 2022 — 10.0.0.161

| Nessus finding (Info) | Report rating | Remediation in my report |
| --- | ---: | --- |
| 45590 — CPE | 2.8 | Maintain OS/software patches; no direct fix for identification. |
| 10736 — DCE services enumeration | 3.1 | Restrict TCP 135 and dynamic RPC to authorized networks. |
| 11002 — DNS server detection | 3.5 | Restrict recursion to trusted clients and disable public zone transfers. |
| 43111 — HTTP methods allowed | 2.5 | Remove unused methods such as TRACE; allow required methods only. |
| NTP service detection — report only | 2.8 | Restrict NTP queries and configure trusted time sources. |
| Default IIS page — report only | 3.4 | Remove default page and unused site; deploy intended applications only. |

NTP and default IIS page are described in my report but are not visible in the supplied Nessus screenshot. Other visible informational entries, including Kerberos, LDAP and LLMNR, have no explicit server-specific remediation in my report. The remaining entries of the 32-result summary are not visible, so I have not inferred plugin IDs or mappings for them.

## Follow-up

Validate firewall changes and required services, repeat the scan, and compare findings. No follow-up scan is included; closure and risk reduction are not claimed.
