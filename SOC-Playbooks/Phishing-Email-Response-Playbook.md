# Phishing Email Incident Response Playbook

**MITRE ATT&CK:** T1566.001 - Spearphishing via Email  
**Type:** SOC Incident Response Playbook  
**Version:** 1.0  
**Author:** Sai Naga Sabarish Yerramsetty  

---

## What This Is

A standardized step by step response guide for SOC analysts when a phishing email is reported. Built from a real phishing investigation involving an email impersonating Banco Bradesco, one of Brazil's largest banks.

The purpose of a playbook is to make the response consistent. Every analyst on the team follows the same process regardless of experience level. That means faster response times, fewer mistakes, and better documentation.

---

## When to Trigger This Playbook

- A user reports receiving a suspicious email
- SIEM alert fires on email authentication triple failure (SPF + DKIM + DMARC all fail simultaneously)
- Email gateway flags an inbound email as suspicious
- EDR detects a malicious attachment being opened on an endpoint
- A user reports clicking a suspicious link

---

## Tools Required

MXToolbox, AbuseIPDB, VirusTotal, Shodan, URLScan, DomainTools WHOIS, ThreatFox, SIEM, Email Gateway

---

## Phase 1: Identification

**Step 1.1 - Acknowledge the report**
Contact the reporting user within 15 minutes. Confirm receipt and tell them not to interact with the email further.

**Step 1.2 - Ask the critical question**
"Did you click any links or download any attachments?"
The answer to this question determines whether you go into containment mode or investigation mode.

**Step 1.3 - Collect the raw email**
Ask the user to save and send the email as a .eml file. Do not ask them to forward it normally as this strips the original headers.

---

## Phase 2: Containment

**If the user clicked a link or downloaded an attachment:**
- Isolate the endpoint from the network immediately
- Disable the user account temporarily
- Notify senior analyst or incident response team
- Preserve all logs before making any changes to the system

**If the user did not click anything:**
- Ask the user to move the email to a designated quarantine folder
- Do not delete the email as it is evidence

---

## Phase 3: Investigation

**Step 3.1 - Analyze email headers**
Open the raw .eml file and paste the full headers into MXToolbox Email Header Analyzer. Look for SPF result, DKIM result, DMARC result, originating IP address, and Return-Path hostname. If SPF, DKIM, and DMARC all fail simultaneously the sender address is almost certainly spoofed.

**Step 3.2 - Investigate the originating IP**
Run the originating IP through AbuseIPDB to check abuse reports and confidence score, VirusTotal to check vendor detections, and Shodan to check open ports, running services, and hosting provider.

**Step 3.3 - Investigate the sender domain**
Run the sender domain through DomainTools WHOIS to check registered owner, creation date, and hosting history. Run it through URLScan to check what infrastructure the domain contacts. Run it through ThreatFox to check if it appears in any known threat reports.

**Step 3.4 - Check scope**
Search the email gateway or SIEM for other users who received the same email from the same sender IP or domain.

---

## Phase 4: Eradication

1. Block the sender domain at the email gateway
2. Block the originating IP at the perimeter firewall
3. Quarantine all similar emails across all user inboxes
4. Delete the phishing email from affected inboxes after evidence is preserved

---

## Phase 5: Recovery

1. Send a user awareness alert to the organization describing the campaign
2. Re-enable any accounts that were disabled during containment after confirming no compromise
3. Submit the malicious IP and domain to AbuseIPDB

---

## Phase 6: Documentation

1. Write the full incident report including timeline, IOCs, tools used, actions taken, and recommendations
2. Update the SIEM detection rule to flag triple authentication failure automatically
3. Brief senior IT leadership with a non-technical summary

---

## Escalation Criteria

Escalate to senior analyst immediately if:
- The user confirmed clicking a link or downloading an attachment
- Multiple users across the organization received the same email
- Credentials may have been entered on a phishing page
- A privileged or executive account was targeted

---

## SIEM Detection Rules

**Email Gateway:**
- Block all inbound email where sender domain matches confirmed malicious domain
- Quarantine emails where SPF and DKIM and DMARC all fail simultaneously

**Firewall:**
- Block inbound and outbound traffic to and from confirmed malicious IPs

**SIEM:**
- Alert when SPF=FAIL AND DKIM=FAIL AND DMARC=FAIL on the same email
- Alert when From domain does not match Return-Path domain
- Alert when Return-Path contains Linux VPS hostname patterns

---

## Real Investigation This Was Built From

This playbook was built from a real phishing investigation involving an email impersonating Banco Bradesco. SPF, DKIM, and DMARC all failed. The originating IP was a DigitalOcean VPS in California with no affiliation to any bank. The sender domain was not owned by Banco Bradesco. The attack mapped to MITRE ATT&CK T1566.001.

Full investigation: [Phishing Email Forensics](../Phishing-Email-Forensics/README.md)

---

## Skills Demonstrated

`Incident Response` `SOC Process Documentation` `Phishing Detection` `Email Forensics` `SIEM Detection Engineering` `MITRE ATT&CK` `Threat Intelligence` `Playbook Development`

---

*Part of my SOC Analyst portfolio.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sabarishy/)*
