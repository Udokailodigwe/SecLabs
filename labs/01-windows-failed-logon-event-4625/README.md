# Lab 01 — Windows Failed Logon (Event 4625)

Initial triage of failed Windows sign-ins for accounts matching `admin*`, hunted in Kibana Discover on a Hack The Box lab.

| | |
| --- | --- |
| Date | 3 Nov 2026, 19:16 (desktop clock on the evidence screenshot) |
| Status | Initial triage complete. Logon type, status code, and source address are not in this capture. |
| Platform | [Hack The Box](https://www.hackthebox.com/) |
| SIEM | Elastic Kibana Discover at `http://10.129.3.91:5601` |
| Data view | `windows*` |
| Log shipper | Winlogbeat 8.6.0 |
| Event | Windows Security `4625` — an account failed to log on |
| Reporting host | `PAW` |
| Query | `event.code:4625 AND user.name: admin*` |
| Hits | 8 |

## Objective

Find failed authentication for administrative-style account names, identify the host that reported them, and separate what the opened documents actually contain from the Windows fields still worth pivoting on.

## Environment

The session in the screenshot is a Linux desktop (Applications, Places, System) with Firefox, reached through VNC. The Hack The Box VPN client address in the panel is `10.10.15.76` (12.8 ms). Firefox then opens Kibana on the lab instance `10.129.3.91`, port `5601`, over HTTP.

Bookmarks visible in that browser: HTB Labs, HTB Certifications, HTB Academy, CTF Platform, Help Center, HTB Blog.

Kibana in this lab is the lab VM's own Elastic install, not Elastic Cloud. The version evidence on the documents is Winlogbeat **8.6.0** and ECS **1.12.0**.

## Result

The query returned **8** failed logons. The histogram piles them in 2023. The two expanded documents are both from **5 Mar 2023**, about six seconds apart (`17:08:59.567` and `17:09:05.379`), both `logon-failed` / `authentication` / `failure`, both shipped by the same Winlogbeat agent on host **`PAW`**.

`PAW` is the privileged access workstation name recorded in `agent.name`. Failed sign-ins for `admin*` accounts on that class of host are a privileged-access lead. The account string itself is highlighted in the screenshot and is not retyped in these notes.

This capture does not show logon type, failure status, source IP, or caller workstation. Those fields decide whether the eight hits are password guessing, a mistyped password, or a service using a stale credential.

## Contents

| Path | What it is |
| --- | --- |
| [docs/log-investigations/event-4625-failed-logon.md](docs/log-investigations/event-4625-failed-logon.md) | Full investigation note |
| [queries/event-4625-admin-failed-logon.kql](queries/event-4625-admin-failed-logon.kql) | Query that was executed, and later pivots marked as not yet run |
| [evidence/kibana-discover-event-4625.png](evidence/kibana-discover-event-4625.png) | Kibana Discover at the time of the hunt |

## ATT&CK

| Technique | How it applies here |
| --- | --- |
| [T1110](https://attack.mitre.org/techniques/T1110/) Brute Force | Lead only. Eight failures against `admin*` names, two of them six seconds apart. Scale, source, and status code are still unread. |
| [T1078](https://attack.mitre.org/techniques/T1078/) Valid Accounts | The hunt was aimed at administrative-style names on a host named `PAW`. Success was not observed. This query is the failure side of that path. |
