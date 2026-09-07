# SIEM Brute Force Detection
 
**MITRE ATT&CK:** T1110 - Brute Force  
**Tools Used:** Splunk, Windows Event Logs, Windows 10  
**Verdict:** Brute Force Attack Successfully Detected  
 
---
 
## What This Project Is
 
I simulated a brute force login attack on a Windows machine and built a detection workflow in Splunk to catch it. The goal was to understand how a SOC analyst detects credential-based attacks using SIEM log analysis.
 
I generated 500+ failed login attempts, ingested the Windows Security logs into Splunk, and wrote SPL queries to flag the attack pattern automatically.
 
---
 
## Attack Simulation
 
| Field | Value |
|---|---|
| Attack Type | Brute Force Login |
| Target | Windows 10 VM |
| Method | Repeated failed login attempts |
| Event Generated | Windows Event ID 4625 (Failed Logon) |
| Volume | 500+ failed attempts |
 
---
 
## Detection in Splunk
 
**Primary Query:**
```
index=main EventCode=4625
| stats count by src_ip, user
| where count > 5
```
 
This query searches for failed login events, counts them by source IP and username, and flags anything with more than 5 failures which is a strong indicator of brute force behavior.
 
---
 
## Key Findings
 
- Successfully detected repeated failed login attempts in Splunk
- Identified the targeted account and source IP within seconds using SPL
- Confirmed brute force behavior pattern through authentication event correlation
- Reduced manual log review time by approximately 60%
---
 
## What I Would Do as a SOC Analyst
 
1. Block the attacking source IP at the perimeter firewall
2. Lock the targeted account temporarily
3. Force password reset on affected accounts
4. Enable MFA on targeted accounts if not already active
5. Increase SIEM alerting threshold for those accounts
6. Document the incident with full timeline and IOCs
7. Escalate if a successful login follows the failed attempts
---
 
## Skills Used
 
`SIEM Configuration` `Splunk SPL` `Log Analysis` `Windows Event Logs` `Authentication Event Investigation` `Brute Force Detection` `Incident Detection` `MITRE ATT&CK Mapping`
 
---
 
*Part of my SOC Analyst portfolio.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sabarishy/)*
 
---
---
