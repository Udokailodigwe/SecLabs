# SecLabs

Security operations lab portfolio. Each lab is a self-contained case folder: a short summary, the investigation note, the query that was run, and the screenshot it came from.

**Author:** Udoka

## Labs

| Lab | Case | Platform | Result |
| --- | --- | --- | --- |
| [01 — Windows failed logon (4625)](labs/01-windows-failed-logon-event-4625/) | Failed sign-ins for `admin*` accounts in Elastic | Hack The Box, Kibana Discover, Winlogbeat | 8 events on host `PAW` |
| [02 — Wazuh on Windows 11](labs/02-wazuh-windows11-vulnerability-detection/) | Wazuh server plus a Windows 11 agent | Wazuh manager, indexer, dashboard | 18 critical findings, CIS score 26% |

## Featured

- **[Windows Failed Logon Investigation (Event 4625)](labs/01-windows-failed-logon-event-4625/docs/log-investigations/event-4625-failed-logon.md)** — Kibana Discover and KQL against the `windows*` data view. 8 failed admin logons on host `PAW`.
- **[Wazuh on Windows 11](labs/02-wazuh-windows11-vulnerability-detection/docs/vulnerability-detection/windows11-host.md)** — Manager, indexer, and dashboard on Ubuntu; agent `Windows11-Host`; 18 critical package findings and a 26% CIS score.

## How a lab is stored

```text
labs/NN-short-name/
├── README.md                  summary: objective, environment, result
├── docs/                      investigation note
├── queries/                   the exact query, plus later pivots marked as such
└── evidence/                  screenshots
```

New labs get the next number. Notes stay tied to a screenshot, and anything that was not on screen is labeled as a next step rather than a finding.
