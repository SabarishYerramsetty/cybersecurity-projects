 
# IOC Report: Banco Bradesco Phishing Campaign
 
**MITRE ATT&CK:** T1566.001 - Spearphishing via Email  
**Tools Used:** ThreatFox, Shodan, URLScan, AbuseIPDB, VirusTotal, STIX 2.1  
**Threat Status:** Active IP, Sender Domain Offline  
 
---
 
## What This Project Is
 
This builds on my phishing email investigation. I took the raw indicators I found and turned them into a structured IOC report, the kind a SOC team would actually use to update firewall rules, SIEM detection logic, and threat intel databases.
 
I ran each IOC through additional threat intelligence platforms to enrich the data and build a more complete picture of the attacker's infrastructure.
 
---
 
## Campaign Overview
 
| Field | Value |
|---|---|
| Campaign | Banco Bradesco Loyalty Points Phishing |
| First Observed | September 19, 2023 |
| Analysis Date | June 2, 2026 |
| Target Region | Brazil |
| Target Sector | Financial Services |
| MITRE ATT&CK | T1566.001 |
| Objective | Credential Harvesting |
| Infrastructure Status | Sender domain offline. Originating IP still active. |
 
---
 
## Indicators of Compromise
 
| IOC | Type | Severity | Confidence | Notes |
|---|---|---|---|---|
| 137.184.34.4 | IP Address | HIGH | HIGH | DigitalOcean VPS. Flagged malicious by Criminal IP. Still active June 2026. |
| atendimento.com.br | Domain | HIGH | HIGH | Not owned by Bradesco. DNS no longer resolves. |
| banco.bradesco@atendimento.com.br | Email | CRITICAL | HIGH | Spoofed sender. SPF/DKIM/DMARC all failed. |
| root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 | Hostname | MEDIUM | HIGH | Return-path Linux VPS hostname. |
| calduct.com | Domain | MEDIUM | MEDIUM | Additional hostname on same IP per Shodan. |
| 1627707.cloudwaysapps.com | Hostname | MEDIUM | MEDIUM | Cloudways hosting on same IP. |
 
---
 
## IP Investigation: 137.184.34.4
 
| Field | Value |
|---|---|
| ISP | DigitalOcean, LLC |
| ASN | AS14061 |
| Cloud Region | US-CA (Santa Clara, California) |
| Open Ports | 22 (SSH), 80 (HTTP), 443 (HTTPS) |
| OS / Service | OpenSSH 9.2p1 on Debian Linux |
| Last Seen Shodan | June 1, 2026 — IP still active |
| URLScan Scans | Scanned 7 times, contacts Amazon S3 CDN |
| AbuseIPDB | 13 reports, 17% confidence score |
| VirusTotal | 1/91 vendors flagged |
| Criminal IP | MALICIOUS |
| GreyNoise | SUSPICIOUS |
| ThreatFox | Not found in database |
 
Port 22 is publicly exposed. Banks do not run mail infrastructure on servers with public SSH access. URLScan also revealed the server contacts Amazon IPs and uses S3 as a CDN, meaning phishing content was likely being served from S3 buckets to appear more legitimate.
 
---
 
## Domain Investigation: atendimento.com.br
 
| Field | Value |
|---|---|
| Registered Owner | Maximilian Gregory Peisker Lacerda |
| Bradesco Affiliation | None |
| Created | 2018-09-20 |
| Name Servers | Hostgator Brazil |
| Hosting History | 7 changes across 6 providers over 8 years |
| Current DNS | FAILED — domain no longer resolves |
| ThreatFox | Not found in database |
 
---
 
## STIX 2.1 Representation
 
```json
{
  "type": "bundle",
  "objects": [
    {
      "type": "indicator",
      "spec_version": "2.1",
      "name": "Malicious IP - Bradesco Phishing",
      "pattern": "[ipv4-addr:value = '137.184.34.4']",
      "pattern_type": "stix",
      "valid_from": "2023-09-19T00:00:00Z",
      "labels": ["malicious-activity", "phishing"]
    },
    {
      "type": "indicator",
      "spec_version": "2.1",
      "name": "Phishing Domain - Bradesco Impersonation",
      "pattern": "[domain-name:value = 'atendimento.com.br']",
      "pattern_type": "stix",
      "valid_from": "2023-09-19T00:00:00Z",
      "labels": ["malicious-activity", "phishing", "brand-impersonation"]
    }
  ]
}
```
 
---
 
## Detection Rules
 
**Email Gateway:**
- Block all email where sender domain = atendimento.com.br
- Quarantine emails where SPF, DKIM, and DMARC all fail together
**Firewall:**
- Block inbound and outbound traffic to/from 137.184.34.4
**SIEM:**
- Alert when SPF=FAIL AND DKIM=FAIL AND DMARC=FAIL simultaneously
- Alert when From domain differs from Return-Path domain
---
 
## Skills Used
 
`Threat Intelligence` `IOC Enrichment` `ThreatFox` `Shodan` `URLScan` `STIX 2.1` `Detection Engineering` `MITRE ATT&CK` `OSINT`
 
---
 
*Part of my SOC Analyst portfolio.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sabarishy/)*
