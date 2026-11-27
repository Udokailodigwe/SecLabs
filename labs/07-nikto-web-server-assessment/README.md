# Lab 07 — Web Server Vulnerability Assessment with Nikto

I used Nikto v2.6.1 on Kali Linux to assess two HTTPS websites and reviewed HTTP response headers to contextualize scanner output.

| | |
| --- | --- |
| Date | 20 November 2026 |
| Platform | Kali Linux |
| Tools | Nikto v2.6.1, curl |
| Targets | Personal GitHub Pages site (`/meet/`) and a secondary website |

## Result

- Personal site: 8,167 requests, 0 errors and 16 reported items in 284 seconds.
- I checked the response headers with curl and observed HTTP 404, limiting conclusions about the intended application.
- I also reviewed partial Nikto output for the secondary website; no completion summary was supplied.

See the [assessment walkthrough](docs/nikto-assessment.md) for numbered evidence.

## Lesson learned

I learned to distinguish scanner observations from confirmed vulnerabilities and validate the response status before interpreting security-header findings.
