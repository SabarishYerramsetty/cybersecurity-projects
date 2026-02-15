# Cybersecurity Projects Portfolio

This repository contains hands-on cybersecurity projects focused on:

- SOC Operations
- Incident Response
- Threat Hunting
- Vulnerability Management
- Risk Assessment

## Projects

### Week 1 – SIEM Log Analysis
# SIEM Brute Force Detection – Windows + Splunk

## Overview
This project demonstrates detection of brute-force login attacks using Windows Event Logs and Splunk SIEM.

## Environment
- Windows 10 VM
- VirtualBox
- Splunk Enterprise

## Attack Simulation
- Created attacker account
- Performed multiple failed logins
- Generated Event ID 4625

## Detection
Search Query:

index=* EventCode=4625

## Findings
Detected 5 failed login attempts targeting the attacker account within a short time window.

## Skills Demonstrated
- SIEM setup
- Log analysis
- Incident response
- Security monitoring

## Status
Completed ✅


### Week 2 – Vulnerability Assessment
📌 Objective

To simulate malware activity using the EICAR test file and analyze Windows Defender alerts using Splunk SIEM.

This project demonstrates endpoint monitoring, SIEM log ingestion, and malware incident analysis.

🛠️ Tools Used

Windows 10 VM (VirtualBox)

Windows Defender

Splunk Enterprise

EICAR Test File

🔍 Project Workflow

Set up Windows virtual machine.

Enabled Windows Defender.

Generated malware alert using EICAR test file.

Verified detection in Event Viewer (Event ID 1116).

Configured Splunk to ingest Defender logs.

Resolved permission issues.

Analyzed malware events in Splunk.

Documented findings.

📊 Splunk Queries Used index=* EventCode=1116

index=* "Windows Defender"

📈 Key Learnings

Endpoint security monitoring

SIEM log onboarding

Windows permission management

Malware investigation

Incident response workflow

Successfully detected and analyzed malware alerts using SIEM and documented the incident professionally.

Status: Completed ✅

### Week 3 – Incident Response Simulation
Status: Planned

### Week 4 – Threat Hunting (MITRE ATT&CK)
Status: Planned


Maintained by: Sai Naga Sabarish Yerramsetty
