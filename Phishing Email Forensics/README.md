# Phishing Email Forensics Analysis

**MITRE ATT&CK:** T1566.001 — Spearphishing via Email  
**Tools Used:** MXToolbox · AbuseIPDB · VirusTotal · DomainTools WHOIS  
**Verdict:** Phishing Confirmed — High Confidence  

---

## Overview

This project documents a full forensic investigation of a real-world phishing email
impersonating **Banco Bradesco**, one of Brazil's largest banks. The email attempted 
to deceive Brazilian customers into clicking a malicious link by claiming their loyalty points were expiring.

The investigation covers email header analysis, IP reputation checking, domain WHOIS
lookup, and threat intelligence correlation — replicating exactly what a SOC analyst would do upon receiving a phishing report.

---

## Email Metadata

| Field | Value |
|---|---|
| Subject | CLIENTE PRIME - BRADESCO LIVELO: Seu cartão tem 92.990 pontos LIVELO expirando hoje! |
| From | BANCO DO BRADESCO LIVELO `<banco.bradesco@atendimento.com.br>` |
| Return-Path | `root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06` |
| Date | Tue, 19 Sep 2023 18:35:49 +0000 |
| Originating IP | 137.184.34.4 |

---

## Email Authentication Results

| Check | Result | Details |
|---|---|---|
| SPF | FAIL | Alignment and authentication both failed |
| DKIM | FAIL | Message not signed, no DKIM record |
| DMARC | FAIL | No DMARC record found for sender domain |

All three authentication mechanisms failed — a definitive indicator of a spoofed sender address.

---

## IP Reputation Analysis (137.184.34.4)

| Field | Value |
|---|---|
| ISP | DigitalOcean, LLC |
| Usage Type | Data Center / Web Hosting / Transit |
| ASN | AS14061 |
| Hostname | 1627707.cloudwaysapps.com |
| Location | Santa Clara, California, USA |
| AbuseIPDB | 13 reports — 17% Confidence of Abuse |
| VirusTotal | 1/91 vendors flagged |
| Criminal IP | MALICIOUS |
| GreyNoise | SUSPICIOUS |
| AlphaSOC | SUSPICIOUS |

> Real financial institutions operate dedicated mail servers under their own infrastructure — not cheap DigitalOcean VPS servers.

---

## Sender Domain Analysis (atendimento.com.br)

| Field | Value |
|---|---|
| Registered Owner | Maximilian Gregory Peisker Lacerda |
| Created | 2018-09-20 |
| Name Servers | Hostgator Brazil |
| IP History | 2 changes over 4 years |
| Hosting History | 7 changes across 6 providers over 8 years |

The domain owner has no affiliation with Banco Bradesco. Hosted on consumer-grade Hostgator 
infrastructure with multiple provider changes — inconsistent with legitimate banking operations.

---

## Suspicious Indicators

- SPF, DKIM, and DMARC all failed — no authentication passed
- Email originated from a DigitalOcean VPS, not a bank mail server
- Return-Path shows `root` user on a Linux cloud server — banks never do this
- Sender domain `atendimento.com.br` is not owned by Banco Bradesco
- Urgency tactic: "92,990 points expiring today" — designed to panic the victim
- IP flagged as MALICIOUS by Criminal IP threat intelligence

---

## Indicators of Compromise (IOCs)

| Type | Value |
|---|---|
| Malicious IP | 137.184.34.4 |
| Fraudulent Domain | atendimento.com.br |
| Spoofed Sender | banco.bradesco@atendimento.com.br |
| Suspicious Return-Path | root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| MITRE ATT&CK | T1566.001 — Spearphishing via Email |

---

## Recommended Actions

1. Block sender domain `atendimento.com.br` at the email gateway
2. Block originating IP `137.184.34.4` at the perimeter firewall
3. Quarantine all emails from this IP range
4. Alert end users about this active phishing campaign
5. Submit IP and domain to AbuseIPDB for community threat intelligence
6. Report to Banco Bradesco abuse team for brand protection action
7. Create SIEM detection rule: flag emails where SPF + DKIM + DMARC all fail simultaneously

---

## Skills Demonstrated

`Email Header Analysis` `Threat Intelligence` `OSINT` `MITRE ATT&CK Mapping` `IOC Identification` 
`Phishing Detection` `AbuseIPDB` `VirusTotal` `WHOIS Analysis` `MXToolbox`

---

*Part of my SOC Analyst portfolio — documenting hands-on cybersecurity investigations.*  
*Connect with me on [LinkedIn](https://www.linkedin.com/in/sai-naga-sabarish-yerramsetty-617013210)*
