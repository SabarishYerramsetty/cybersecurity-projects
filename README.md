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
Status: Planned

### Week 3 – Incident Response Simulation
Status: Planned

### Week 4 – Threat Hunting (MITRE ATT&CK)
Status: Planned


Maintained by: Sai Naga Sabarish Yerramsetty
