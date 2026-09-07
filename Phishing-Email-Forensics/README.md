
# Phishing Email Incident Response Playbook
 
**MITRE ATT&CK:** T1566.001 - Spearphishing via Email  
**Type:** SOC Incident Response Playbook  
**Version:** 1.0  
 
---
 
## What This Is
 
A standardized step by step response guide for SOC analysts when a phishing email is reported. Built from a real phishing investigation involving an email impersonating Banco Bradesco. Ensures consistent response regardless of which analyst handles the incident.
 
---
 
## When to Use This Playbook
 
- A user reports receiving a suspicious email
- SIEM alert fires on email authentication triple failure
- Email gateway flags an inbound email as suspicious
- EDR detects a malicious attachment being opened
- User reports clicking a suspicious link
---
 
## Response Phases
 
### Phase 1: Identification
1. Acknowledge the report within 15 minutes
2. Ask the user: did you click any links or download any attachments?
3. Ask the user to forward the raw email as a .eml file
### Phase 2: Containment
**If the user clicked anything:**
- Isolate the endpoint from the network immediately
- Disable the user account temporarily
- Notify senior analyst
- Preserve all logs before making changes
**If the user did not click anything:**
- Ask user to move the email to a quarantine folder
- Do not delete the email as it is evidence
### Phase 3: Investigation
1. Paste raw headers into MXToolbox and check SPF, DKIM, DMARC
2. Run originating IP through AbuseIPDB, VirusTotal, and Shodan
3. Run sender domain through DomainTools WHOIS and URLScan
4. Search email gateway logs for other users who received the same email
### Phase 4: Eradication
1. Block sender domain at the email gateway
2. Block originating IP at the perimeter firewall
3. Quarantine similar emails across all inboxes
4. Delete the phishing email after evidence is preserved
### Phase 5: Recovery
1. Send a user awareness alert to the organization
2. Re-enable any accounts disabled during containment after investigation is complete
3. Submit malicious IP and domain to AbuseIPDB
### Phase 6: Documentation
1. Write the full incident report with timeline, IOCs, and actions taken
2. Update SIEM detection rule to flag triple authentication failure
3. Brief senior leadership with a non-technical summary
---
 
## Escalate Immediately If
 
- User clicked a link or downloaded an attachment
- Multiple users received the same email
- Any credentials may have been entered on a phishing page
- A privileged or executive account was targeted
---
 
## Skills Demonstrated
 
`Incident Response` `SOC Process Documentation` `Phishing Detection` `Email Forensics` `SIEM Detection Engineering` `MITRE ATT&CK` `Threat Intelligence`
 
---
 
*Part of my SOC Analyst portfolio.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sai-naga-sabarish-yerramsetty-617013210)*
 
---
---
 
# Brute Force Attack Incident Response Playbook
 
**MITRE ATT&CK:** T1110 - Brute Force  
**Type:** SOC Incident Response Playbook  
**Version:** 1.0  
 
---
 
## What This Is
 
A standardized step by step response guide for SOC analysts when a brute force attack is detected. Built from a real lab simulation where 500+ failed login attempts were detected through Event ID 4625 in Splunk. Ensures consistent response regardless of which analyst handles the incident.
 
---
 
## When to Use This Playbook
 
- SIEM alert fires on 5 or more failed logins from the same IP within 5 minutes
- Failed login attempts detected outside business hours
- Account lockout triggered on a privileged account
- Failed logins followed by a successful login from the same IP
---
 
## Key Event IDs
 
| Event ID | Name | When to Act |
|---|---|---|
| 4625 | Failed Logon | Core detection trigger. Alert on 5+ from same IP in 5 min. |
| 4624 | Successful Logon | Critical if it follows 4625 alerts. Possible breach. |
| 4740 | Account Locked Out | Check if the locked account is privileged. |
| 4688 | Process Created | Check after successful login for attacker tools. |
| 4663 | File Accessed | Check for data access after successful login. |
 
---
 
## Response Phases
 
### Phase 1: Identification
1. Run Splunk query to confirm brute force activity:
```
index=main EventCode=4625
| stats count by src_ip, user
| where count > 5
```
2. Check if any failed attempts were followed by a successful login
3. Identify how many accounts and systems are targeted
### Phase 2: Containment
**If a successful login was detected:**
- Disable the compromised account immediately
- Isolate the endpoint
- Escalate to senior analyst immediately
**If no successful login:**
- Block the attacking source IP at the firewall
- Temporarily lock targeted accounts
- Increase SIEM alerting on those accounts
### Phase 3: Investigation
1. Run attacking IP through AbuseIPDB and VirusTotal
2. Analyze the attack pattern — is it automated or manual?
3. Check for lateral movement if successful login occurred
4. Search for the same attacking IP across other systems
### Phase 4: Eradication
1. Block attacking IP at the perimeter firewall
2. Force password reset on all targeted accounts
3. Enable account lockout policy if not already configured
4. Enforce MFA on targeted accounts
### Phase 5: Recovery
1. Re-enable locked accounts after credentials are reset
2. Verify system integrity if any account was compromised
3. Notify affected users about the attack and credential reset
### Phase 6: Documentation
1. Write the full incident report with timeline and IOCs
2. Update SIEM detection rule threshold based on findings
3. Brief senior leadership if accounts were compromised
---
 
## Escalate Immediately If
 
- A successful login followed brute force attempts from the same IP
- A privileged or admin account was targeted or compromised
- The attack is targeting multiple systems simultaneously
- Signs of lateral movement are detected after a successful login
---
 
## Skills Demonstrated
 
`Incident Response` `SOC Process Documentation` `Brute Force Detection` `Splunk SPL` `Windows Event Log Analysis` `SIEM Detection Engineering` `MITRE ATT&CK`
 
---
 
*Part of my SOC Analyst portfolio.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sabarishy/)*
