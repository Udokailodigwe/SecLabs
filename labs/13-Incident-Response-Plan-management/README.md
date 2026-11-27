# Lab 13 — Cybersecurity Incident Management & Response Planning

**Classification:** Incident Response Planning & Security Governance  
**Research basis:** Mandiant — AI Risk and Resilience 2026  
**Environment:** AI-integrated development systems, software supply chains and cloud infrastructure.

## 1. Objective

Developed an Incident Management Plan addressing AI-enabled cybersecurity threats, defining response procedures, escalation protocols, service recovery priorities and organizational responsibilities.

## 2. Identified Incidents

- AI coding assistant hijacking and prompt injection.
- Shai-Hulud worm and malicious software dependencies.
- Compromised CI/CD credentials and unauthorized cloud access.
- Potential malware propagation and sensitive data exfiltration.

## 3. Plan Activation

Activate the plan for High (P2) or Critical (P1) incidents, or when credible evidence indicates a risk of widespread compromise.

## 4. Critical Services and Recovery Objectives

| Priority | Critical service | Target RTO |
| --- | --- | --- |
| P1 — Critical | Identity and authentication | 1 hour |
| P1 — Critical | Production infrastructure, SIEM and EDR | 2 hours |
| P2 — High | Repositories, CI/CD and secrets management | 4 hours |
| P3 — Medium | AI assistants and package registries | 8 hours |
| P4 — Low | Non-production environments | 24–48 hours |

## 5. Roles and Responsibilities

| Role | Responsibility |
| --- | --- |
| CISO | Executive oversight and approval |
| Incident Response Manager | Plan activation and response coordination |
| SOC Team | Detection, triage and escalation |
| DFIR Team | Forensic investigation and evidence preservation |
| Cloud Security & DevSecOps | Technical containment and remediation |
| Business Continuity Manager | Service continuity and recovery |
| Legal & Compliance | Regulatory and breach notification |

## 6. Incident Response Lifecycle

| Phase | Response action |
| --- | --- |
| Preparation | Establish response procedures, asset inventories and responsibilities. |
| Detection & Analysis | Investigate SIEM, EDR, cloud, repository and AI activity logs. |
| Containment | Isolate compromised systems, revoke credentials and quarantine malicious dependencies. |
| Eradication | Remove malicious components and remediate compromised configurations. |
| Recovery | Restore trusted systems and validate integrity against recovery objectives. |
| Lessons Learned | Conduct root cause analysis and implement corrective controls. |

## 7. Communication and Escalation

Defined secure communication channels, incident ticketing, emergency escalation, stakeholder notifications and alternative communication arrangements.

## 8. Evidence and Critical Assets

Identified essential investigation resources, including security logs, cloud audit trails, repository histories, AI execution logs, SBOMs and forensic evidence. Established evidence integrity, confidentiality and chain-of-custody requirements.

## 9. Recommended Security Controls

Dependency verification, short-lived credentials, least-privilege access, isolated AI execution, restricted network egress and continuous SIEM/EDR monitoring.

## 10. Plan Testing and Maintenance

Proposed quarterly tabletop exercises, annual incident response simulations and periodic reviews following significant incidents or infrastructure changes.

## 11. Outcome

Produced a structured Incident Management Plan integrating threat intelligence, incident response, security governance, business continuity and disaster recovery requirements.

**Scope:** Research-based planning exercise. Recovery targets and testing schedules are proposed, not measured results. The plan has not yet been tested.
