# Windows Authentication Event Analysis

## 1. Objective

The objective of this investigation was to review Windows Security authentication events, examine a failed logon, and determine whether the available evidence supported a security concern.

The investigation focused on Windows Security Event IDs **4624** and **4625**, which record successful and failed logon attempts, respectively.

## 2. Tools and Data Sources

- Windows Event Viewer
- Windows Security event logs
- PowerShell
- Windows error-code lookup using `certutil`
- Smart card-related Windows event logs

## 3. Investigation Findings

### Failed Logon Event

One relevant failed logon event was identified with the following details:

| Field | Observation |
|---|---|
| Event ID | 4625 |
| Timestamp | October 28, 2026, at approximately 4:25:53 PM |
| Logon Type | 2 — Interactive logon |
| Process | `C:\Windows\System32\svchost.exe` |
| Source Address | `127.0.0.1` |
| Status | `0xC000006D` |
| SubStatus | `0xC0000380` |

The target username was not identified in the available event details.

### Error-Code Analysis

I used the Windows error-code lookup command to investigate substatus `0xC0000380`.

The result identified the status as `STATUS_SMARTCARD_WRONG_PIN`, indicating that an incorrect PIN was presented to a smart card.

This finding suggests that the failed authentication was related to a smart card PIN. However, the available evidence does not establish who initiated the attempt or why it occurred.

### Nearby Successful Logons

Successful logon events were also observed approximately six seconds after the failed event. These included logon types 7 and 11 associated with a Microsoft account.

A service logon event, type 5, was recorded shortly afterward.

Although these events occurred close together in time, temporal proximity alone does not prove that they were directly related to the failed smart card authentication.

## 4. Additional Log Review

I reviewed relevant smart card event logs for activity around the time of the failed logon.

- The SmartCard-DeviceEnum/Operational log contained records, but none were found in the reviewed 4:20–4:30 PM window.
- The SmartCard-Audit/Authentication log contained no records.
- The SmartCard-TPM-VCard log contained no records.
- The CAPI2 log was disabled.

These results limited the amount of additional evidence available to correlate with the authentication event.

## 5. Assessment

The evidence supports the conclusion that a failed authentication event reported a smart card PIN error. However, the available records were insufficient to determine whether the event represented an ordinary user error, an application-related authentication attempt, or suspicious activity.

The nearby successful logons were noted but were not conclusively linked to the failed event.

**Final assessment: Inconclusive. The reviewed evidence does not establish malicious activity.**

## 6. Recommended Follow-Up

If this event occurred in a production environment, the next steps would include:

1. Review the complete Event ID 4625 record, including the account name, authentication package, and other available fields.
2. Correlate the timestamp with related logon, process, and smart card events.
3. Confirm whether smart card authentication was expected on the system.
4. Review additional events for repeated failures or other unusual authentication patterns.
5. Escalate the investigation if corroborating evidence indicates unauthorized access or repeated suspicious behavior.

## 7. Skills Demonstrated

- Windows Security event log analysis
- PowerShell-based event querying
- Windows authentication status-code investigation
- Event correlation and timeline analysis
- Evidence-based security triage
- Technical documentation and cautious reporting

## 8. Conclusion

This investigation provided practical experience examining Windows authentication events and interpreting a failed logon status. It also demonstrated the importance of correlating events, recognizing gaps in available telemetry, and avoiding conclusions that the evidence does not support.

The investigation was documented as a learning exercise. No claim of confirmed compromise or malicious activity is made.
