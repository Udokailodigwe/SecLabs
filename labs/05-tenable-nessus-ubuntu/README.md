# Lab 05 — Tenable Nessus on Ubuntu

I deployed Nessus on Ubuntu, scanned three lab assets, reviewed the findings, and prepared a vulnerability assessment and remediation report.

| | |
| --- | --- |
| Scanner | Ubuntu, `10.0.0.146` |
| Product | Tenable Nessus Essentials Plus |
| Console | `https://10.0.0.146:8834` |
| Evidence | Service verification on 11 Nov 2026; scan report dates not shown |

## Results

| Target | Critical | High | Medium | Low | Info | Total |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Kali Linux (`10.0.0.145`) | 0 | 0 | 1 | 0 | 5 | 6 |
| Windows 11 host (`10.0.0.159`) | 0 | 0 | 0 | 0 | 7 | 7 |
| Windows Server 2022 (`10.0.0.161`) | 0 | 0 | 0 | 0 | 32 | 32 |
| **Total** | **0** | **0** | **1** | **0** | **44** | **45** |

The medium finding was ICMP Timestamp Request Remote Date Disclosure (plugin 10114, CVSS 4.0). I prioritized firewall restrictions and reviewed informational findings for unnecessary service exposure. No post-remediation scan is supplied.

## Contents

| Path | Description |
| --- | --- |
| [Assessment walkthrough](docs/nessus-assessment.md) | Deployment and three scan summaries in workflow order |
| [Remediation mapping](docs/remediation-mapping.md) | Report recommendations matched to visible Nessus plugins |
| [Original VA report](reports/va-remediation-report.docx) | My original assessment report |
| [Evidence](evidence/) | Four numbered screenshots |

**Lesson:** Scanner severity, service exposure and business risk are different; remediation should be validated with a follow-up scan.
