# Incident 002 — Blocked SMTP Connection in Ubuntu WSL

**Status:** Investigation documented  
**Environment:** Ubuntu on WSL with Windows host connectivity test  
**Service/port:** Postfix SMTP, TCP port 25

## Objective

Determine why a Windows host connection test to the Ubuntu WSL address on TCP port 25 failed even though Postfix appeared to be listening inside Ubuntu.

## Evidence reviewed

- Nmap against localhost showed TCP port 25 open in the Ubuntu environment.
- Postfix's SMTP master process was listening on `0.0.0.0:25`.
- UFW was active, with incoming traffic denied by default.
- The configured rules included an outbound allowance for port 25, but no corresponding inbound allowance was shown.
- A Windows `Test-NetConnection` to the WSL IP on port 25 failed.
- UFW logs showed a blocked incoming TCP SYN from the Windows-side WSL virtual interface to destination port 25.

## Assessment

The evidence is consistent with the incoming connection being blocked by the Ubuntu UFW firewall. A service listening inside the Linux environment does not by itself guarantee that a connection from the Windows host will be permitted through the firewall and WSL networking path.

## Safe response

Do not disable the firewall just to make the test succeed. First confirm whether inbound SMTP access is actually required, understand the exposure, and make any rule change only as a deliberate, narrow, reversible lab change. For this exercise, the firewall was left enabled.

## Limitations

- This was a lab connectivity investigation, not a production network assessment.
- WSL networking behavior can vary by configuration.
- No conclusion is made about external network reachability.

## Lessons learned

- Separate service-listener checks from host-to-service connectivity checks.
- Read firewall logs alongside connection-test results.
- Confirm the need and scope before allowing inbound traffic.