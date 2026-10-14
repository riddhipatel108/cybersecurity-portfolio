# SOC Home Lab

**Status: In progress**

## Goal

Build practical experience generating, collecting, and investigating security telemetry in a controlled home lab, then document findings in a clear, repeatable format.

## Current work

- Windows Sysmon installation and event review.
- PowerShell logging tests and controlled test strings.
- Review of process-creation and network-related telemetry.
- Ubuntu WSL service and UFW firewall troubleshooting.
- Investigation write-ups that separate observations from assumptions.

## Tools practiced

- Windows Event Viewer
- Sysmon
- PowerShell
- Ubuntu on WSL
- Postfix service checks
- UFW firewall rules and logs
- Basic TCP port and connectivity checks

## Documented investigations

1. [Incident 001 — Windows process review](reports/incident-001-windows-process-review.md)
2. [Incident 002 — Blocked SMTP connection](reports/incident-002-blocked-smtp.md)

## Planned next steps

- Complete a controlled Windows authentication-event exercise.
- Add sanitized screenshots or sample event fields where useful.
- Document detection logic, triage decisions, and limitations.
- Consider adding a SIEM component once the current fundamentals are repeatable.

## Safety and scope

This is a learning lab. Activities should remain on systems the owner controls or is authorized to test. Do not publish secrets, raw private logs, or sensitive device/network information. The project is not presented as a production SOC deployment.