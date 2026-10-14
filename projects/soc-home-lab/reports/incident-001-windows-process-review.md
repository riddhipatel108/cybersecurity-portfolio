# Incident 001 — Windows Process Review

**Status:** Investigation documented  
**Environment:** Personal Windows SOC lab  
**Primary telemetry:** Sysmon Process Create (Event ID 1), with contextual process/service checks

## Objective

Practice reviewing a process-creation event and recording what the available evidence supports without treating an unfamiliar process as malicious by default.

## Investigation steps

1. Located a Sysmon Event ID 1 record for `WmiPrvSE.exe`.
2. Reviewed the executable path and command-line information available in the event.
3. Examined the recorded parent-process context.
4. Used PowerShell to inspect the current `svchost.exe` process and associated service information as a contextual check.
5. Recorded the observations and limits of the investigation.

## Observations

- A process-creation event was available for review.
- The event supplied process metadata such as image/path, command line, and parent-process information.
- Additional process/service checks provided context, but a current process snapshot does not necessarily prove the state of a process at the historical event time.

## Assessment

The available checks support documenting the process and its context, but the event alone is not enough to claim malicious activity. A stronger conclusion would require validating the complete event fields, timestamp, file signature/hash, surrounding process and network events, and whether the behavior was expected in this environment.

## Limitations

- This report summarizes a learning exercise, not a production incident.
- No claim of confirmed compromise is made.
- Screenshots and raw logs are omitted to avoid exposing unnecessary device-specific details.

## Lessons learned

- Correlate process events with parent and child process context.
- Distinguish historical event evidence from current system state.
- State uncertainty explicitly and avoid overclaiming.

## Next steps

If repeating the exercise, preserve the relevant event fields, verify the executable's signature and hash, and correlate events within a clearly defined time window.