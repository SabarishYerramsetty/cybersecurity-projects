# Phishing Email Forensics Analysis

**MITRE ATT&CK:** T1566.001 — Spearphishing via Email  
**Tools Used:** MXToolbox, AbuseIPDB, VirusTotal, DomainTools WHOIS  
**Verdict:** Phishing Confirmed, High Confidence  

---

## What This Project Is

I analyzed a real phishing email that was impersonating Banco Bradesco, one of Brazil's largest banks. The email told victims their loyalty points were about to expire and pushed them to click a link. Classic urgency tactic.

I went through the full investigation process a SOC analyst would run: pulled the raw headers, traced the originating IP, checked threat intelligence platforms, and looked up the sender domain. This is the write-up of what I found.

---

## Email Metadata

| Field | Value |
|---|---|
| Subject | CLIENTE PRIME - BRADESCO LIVELO: Seu cartao tem 92.990 pontos LIVELO expirando hoje! |
| From | BANCO DO BRADESCO LIVELO `<banco.bradesco@atendimento.com.br>` |
| Return-Path | `root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06` |
| Date | Tue, 19 Sep 2023 18:35:49 +0000 |
| Originating IP | 137.184.34.4 |

---

## Email Authentication

| Check | Result | Details |
|---|---|---|
| SPF | FAIL | Alignment and authentication both failed |
| DKIM | FAIL | Message not signed, no DKIM record found |
| DMARC | FAIL | No DMARC record exists for the sender domain |

All three failed. That alone tells you something is wrong. Legitimate banks have SPF, DKIM, and DMARC properly configured because email authentication is a basic security requirement for any financial institution.

---

## IP Reputation Analysis (137.184.34.4)

| Field | Value |
|---|---|
| ISP | DigitalOcean, LLC |
| Usage Type | Data Center / Web Hosting |
| ASN | AS14061 |
| Hostname | 1627707.cloudwaysapps.com |
| Location | Santa Clara, California, USA |
| AbuseIPDB | 13 abuse reports, 17% confidence score |
| VirusTotal | 1/91 vendors flagged |
| Criminal IP | Malicious |
| GreyNoise | Suspicious |
| AlphaSOC | Suspicious |

The email came from a DigitalOcean VPS in California. Banks do not send customer emails from cheap cloud servers. The return path also showed `root@ubuntu-s-1vcpu-...` which is a Linux VPS hostname. No real bank would have that in an email header.

---

## Sender Domain Analysis (atendimento.com.br)

| Field | Value |
|---|---|
| Registered Owner | Maximilian Gregory Peisker Lacerda |
| Created | 2018-09-20 |
| Name Servers | Hostgator Brazil |
| IP History | 2 changes over 4 years |
| Hosting History | 7 changes across 6 providers over 8 years |

The domain owner is not affiliated with Banco Bradesco in any way. It is hosted on Hostgator, which is consumer shared hosting. The seven hosting provider changes over eight years is also a red flag as legitimate business infrastructure does not move around that often.

---

## What Gave It Away

- SPF, DKIM, and DMARC all failed at once
- Email came from a DigitalOcean VPS, not a bank server
- Return-Path showed a Linux VPS root user
- Sender domain not owned by Banco Bradesco
- Urgency tactic: "points expiring today" to pressure the victim into clicking fast
- IP flagged as malicious by Criminal IP

---

## Indicators of Compromise

| Type | Value |
|---|---|
| Malicious IP | 137.184.34.4 |
| Fraudulent Domain | atendimento.com.br |
| Spoofed Sender | banco.bradesco@atendimento.com.br |
| Suspicious Return-Path | root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| MITRE ATT&CK | T1566.001 |

---

## What I Would Do as a SOC Analyst

1. Block the sender domain at the email gateway
2. Block the originating IP at the firewall
3. Quarantine other emails from that IP range
4. Send a user alert about the campaign
5. Report the IP and domain to AbuseIPDB
6. Contact Banco Bradesco abuse team so they can take action
7. Write a detection rule in the SIEM to flag emails where SPF, DKIM, and DMARC all fail together

---

## Skills Used

`Email Header Analysis` `Threat Intelligence` `OSINT` `MITRE ATT&CK Mapping` `IOC Identification` `Phishing Detection` `AbuseIPDB` `VirusTotal` `WHOIS Lookup` `MXToolbox`

---

*Part of my SOC Analyst portfolio.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sai-naga-sabarish-yerramsetty-617013210)*
