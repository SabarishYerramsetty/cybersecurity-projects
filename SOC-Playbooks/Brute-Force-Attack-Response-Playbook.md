# Brute Force Attack Incident Response Playbook

**MITRE ATT&CK:** T1110 - Brute Force  
**Type:** SOC Incident Response Playbook  
**Version:** 1.0  
**Author:** Sai Naga Sabarish Yerramsetty  

---

## What This Is

A standardized step by step response guide for SOC analysts when a brute force attack is detected. Built from a real lab simulation where 500+ failed login attempts were generated against a Windows machine and detected through Event ID 4625 in Splunk.

The goal of this playbook is to make sure the analyst catches the attack early, contains it before any account is compromised, and documents everything properly for the incident report.

---

## When to Trigger This Playbook

- SIEM alert fires on 5 or more failed logins from the same source IP within 5 minutes
- Failed login attempts detected outside business hours
- Account lockout triggered on a privileged or admin account
- Failed logins followed immediately by a successful login from the same IP
- Event ID 4625 count exceeds threshold in Windows Security logs

---

## Tools Required

Splunk, Windows Event Logs, AbuseIPDB, VirusTotal, Firewall, Active Directory

---

## Key Event IDs

| Event ID | Name | When to Act |
|---|---|---|
| 4625 | Failed Logon | Core detection trigger. Alert on 5+ from same IP in 5 minutes. |
| 4624 | Successful Logon | Critical if it follows 4625 alerts from the same IP. Possible breach. |
| 4740 | Account Locked Out | Check immediately if the locked account is privileged or admin. |
| 4648 | Logon with Explicit Credentials | May indicate credential reuse or pass-the-hash attack. |
| 4688 | Process Created | Check for attacker tools after a successful login. |
| 4663 | File Accessed | Check for data access or exfiltration after successful login. |

---

## Phase 1: Identification

**Step 1.1 - Confirm the alert**
Run the following Splunk query to confirm brute force activity:
```
index=main EventCode=4625
| stats count by src_ip, user
| where count > 5
```
Verify it is not a false positive from a legitimate user mistyping their password.

**Step 1.2 - Check for successful login**
Run this query immediately:
```
index=main (EventCode=4625 OR EventCode=4624)
| stats count by src_ip, user, EventCode
```
A successful login after multiple failures from the same IP is a critical escalation trigger.

**Step 1.3 - Determine scope**
Check how many accounts were targeted, how many source IPs are involved, and whether any targeted accounts are privileged or admin accounts.

---

## Phase 2: Containment

**If a successful login was detected after brute force attempts:**
- Disable the compromised account immediately
- Isolate the endpoint the attacker logged into
- Escalate to senior analyst immediately
- Preserve all logs before making any changes

**If no successful login was detected:**
- Block the attacking source IP at the perimeter firewall
- Temporarily lock the targeted accounts if the attack is ongoing
- Increase SIEM alerting threshold for those accounts

---

## Phase 3: Investigation

**Step 3.1 - Investigate the source IP**
Run the attacking IP through AbuseIPDB and VirusTotal. Check if it is a known scanner, VPN exit node, Tor exit node, or data center IP.

**Step 3.2 - Analyze the attack pattern**
Is the attack sequential and fast (automated tool) or scattered over hours (manual attempt)? Is it targeting one specific account or cycling through a username list? This tells you whether it is a targeted attack or a credential stuffing campaign.

**Step 3.3 - Check for lateral movement**
If a successful login occurred, check for file access events (Event ID 4663), new process creation (Event ID 4688), network connections from the compromised account, and any privilege escalation attempts.

**Step 3.4 - Check other systems**
Search the SIEM for the same attacking IP across all other systems. Brute force attacks rarely target just one machine.

---

## Phase 4: Eradication

1. Block the attacking IP at the perimeter firewall, both inbound and outbound
2. Force password reset on all accounts that were targeted
3. Enable account lockout policy if not already configured (5 failed attempts, 30 minute lockout)
4. Enforce MFA on targeted accounts

---

## Phase 5: Recovery

1. Re-enable accounts locked during containment after credentials are reset
2. Verify system integrity if any account was compromised, check for new accounts, scheduled tasks, and registry run keys
3. Notify affected users about the attack and provide password guidance

---

## Phase 6: Documentation

1. Write the full incident report with timeline, source IPs, targeted accounts, and actions taken
2. Update the SIEM detection rule threshold based on findings
3. Brief senior leadership if any account was compromised

---

## Escalation Criteria

Escalate to senior analyst immediately if:
- A successful login followed brute force attempts from the same IP
- A privileged or admin account was targeted or compromised
- The attack is targeting multiple systems simultaneously
- Signs of lateral movement are detected after a successful login
- The attacking IP is associated with a known threat actor

---

## SIEM Detection Rules

**Primary Detection:**
- Alert: EventCode=4625 count greater than 5 from same src_ip within 5 minutes
- Alert: EventCode=4625 occurring outside business hours (12 AM to 6 AM)

**Escalation Rules:**
- Critical Alert: EventCode=4625 followed by EventCode=4624 from same src_ip within 10 minutes
- Critical Alert: EventCode=4740 on any admin or privileged account

---

## Real Lab This Was Built From

This playbook was built from a brute force detection lab where 500+ failed login attempts were simulated on a Windows machine and detected through Splunk using Event ID 4625. The SPL detection query reduced manual log review time by approximately 60%.

Full lab write-up: [SIEM Brute Force Detection](../SIEM-Brute-Force-Detection/README.md)

---

## Skills Demonstrated

`Incident Response` `SOC Process Documentation` `Brute Force Detection` `Splunk SPL` `Windows Event Log Analysis` `SIEM Detection Engineering` `MITRE ATT&CK` `Playbook Development`

---

*Part of my SOC Analyst portfolio.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sabarishy/)*
