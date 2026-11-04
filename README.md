# SecLabs

Security operations lab portfolio. Each lab is a self-contained case folder: a short summary, the investigation note, the query that was run, and the screenshot it came from.

**Author:** Udoka

## Labs

| Lab | Case | Platform | Result |
| --- | --- | --- | --- |
| [01 — Windows failed logon (4625)](labs/01-windows-failed-logon-event-4625/) | Failed sign-ins for `admin*` accounts in Elastic | Hack The Box, Kibana Discover, Winlogbeat | 8 events on host `PAW` |

## Featured

- **[Windows Failed Logon Investigation (Event 4625)](labs/01-windows-failed-logon-event-4625/docs/log-investigations/event-4625-failed-logon.md)** — Kibana Discover and KQL against the `windows*` data view. The note records the access path, the tool versions on screen, the two events that were expanded, and the fields still left to pivot on.

## How a lab is stored

```text
labs/NN-short-name/
├── README.md                  summary: objective, environment, result
├── docs/
│   └── log-investigations/    the investigation note
├── queries/                   the exact query, plus later pivots marked as such
└── evidence/                  screenshots
```

New labs get the next number. Notes stay tied to a screenshot, and anything that was not on screen is labeled as a next step rather than a finding.
