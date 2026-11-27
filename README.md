# SecLabs

Security operations lab portfolio. Each case folder documents the objective, environment, observed result, and screenshots in investigation order. Lab observations are not represented as production findings.

**Author:** Udoka

## Labs

| Lab | Case | Platform | Result |
| --- | --- | --- | --- |
| [01 — Windows failed logon (4625)](labs/01-windows-failed-logon-event-4625/) | Failed sign-ins for `admin*` accounts in Elastic | Hack The Box, Kibana Discover, Winlogbeat | 8 events on host `PAW` |
| [02 — Wazuh on Windows 11](labs/02-wazuh-windows11-vulnerability-detection/) | Wazuh server plus a Windows 11 agent | Wazuh manager, indexer, dashboard | 18 critical findings, CIS score 26% |
| [03 — Windows Server and Active Directory](labs/03-windows-server-active-directory/) | Domain `udokaudodigwe.com` on Hyper-V | Windows Server 2025, Windows 11, AD DS, DHCP, WDS | DC01 and domain-joined WKSTN01 |
| [04 — Nmap and Wireshark scan patterns](labs/04-nmap-wireshark-reconnaissance-scan-patterns/) | TCP connect versus half-open SYN scan | Kali, Nmap 7.99, Wireshark, Firefox | 22 open ports; handshake difference on port 80 |
| [05 — Tenable Nessus on Ubuntu](labs/05-tenable-nessus-ubuntu/) | Scanner deployment, three asset scans and remediation reporting | Nessus Essentials Plus, Ubuntu | 45 findings: 1 medium, 44 informational |
| [06 — OpenVAS assessment on Kali](labs/06-openvas-kali-vulnerability-assessment/) | GVM setup, scanning, result analysis | Kali, GVM/OpenVAS, Nmap-related checks | 12 displayed results: 1 medium, 1 low, 10 log; report at 84% |
| [07 — Nikto web server assessment](labs/07-nikto-web-server-assessment/) | HTTPS web server scanning and response validation | Kali, Nikto, curl | 16 reported items on personal site; HTTP 404 verified |
| [08 — Multi-tool vulnerability assessment](labs/08-multi-tool-vulnerability-assessment/) | Alpine host and web application assessment | OpenVAS, Wapiti, Nikto, WPScan, SQLmap | 5 Wapiti findings; 9 Nikto items; injection test inconclusive |

## Featured

- **[Windows Failed Logon Investigation (Event 4625)](labs/01-windows-failed-logon-event-4625/docs/log-investigations/event-4625-failed-logon.md)** — Kibana Discover and KQL against the `windows*` data view. 8 failed admin logons on host `PAW`.
- **[Wazuh on Windows 11](labs/02-wazuh-windows11-vulnerability-detection/docs/vulnerability-detection/windows11-host.md)** — Manager, indexer, and dashboard on Ubuntu; agent `Windows11-Host`; 18 critical package findings and a 26% CIS score.
- **[Windows Server and Active Directory](labs/03-windows-server-active-directory/docs/project.md)** — DC01 and WKSTN01: AD DS, DHCP, WDS, Marketing Lockdown, share permissions, and WinRM.
- **[Nmap and Wireshark scan patterns](labs/04-nmap-wireshark-reconnaissance-scan-patterns/docs/scan-patterns.md)** — Port discovery, SYN scanning, completed handshakes, and HTTP traffic.
- **[Tenable Nessus assessment](labs/05-tenable-nessus-ubuntu/docs/nessus-assessment.md)** — Verified scanner deployment, assessed three assets, and mapped remediation recommendations to scan findings.
- **[OpenVAS assessment on Kali](labs/06-openvas-kali-vulnerability-assessment/docs/kali-assessment.md)** — GVM start, scan tasks, progress, risk ratings, and DCE/RPC detection on a Windows host.

- **[Nikto web server assessment](labs/07-nikto-web-server-assessment/docs/nikto-assessment.md)** — Web server scanning and HTTP response validation.

- **[Multi-tool vulnerability assessment](labs/08-multi-tool-vulnerability-assessment/docs/assessment.md)** — Scanner comparison, evidence review and remediation recommendations.

## How a lab is stored

```text
labs/NN-short-name/
├── README.md                  objective, environment, result
├── docs/                      evidence-led walkthrough
├── queries/                   only where an actual query was documented
└── evidence/                  numbered screenshots in workflow order
```

Only observed results are reported. Interrupted scans, unverified findings, and future investigative steps are clearly distinguished from completed assessments.
