# Cybersecurity Projects Portfolio

This repository contains hands-on cybersecurity projects focused on:

- SOC Operations
- Incident Response
- Threat Hunting
- Vulnerability Management
- Risk Assessment

## Projects

Week 1 – SIEM Log Analysis
Brute Force Detection – Windows + SIEM

Overview
•	Detect brute-force login attempts using Windows Event Logs.
•	Analyze authentication failures using SIEM monitoring.

Environment
•	Windows 10 VM
•	VirtualBox
•	SIEM platform

Attack / Activity Simulation
•	Created attacker account.
•	Performed multiple failed login attempts.
•	Generated Windows Event ID 4625 (failed logon).

Detection / Analysis
•	Ingested Windows security logs into SIEM.
•	Queried failed authentication events.

Search Query:
•	index=* EventCode=4625

Findings
•	Detected multiple failed login attempts.
•	Identified targeted account activity within a short time window.
•	Confirmed brute-force behavior pattern.

Skills Demonstrated
•	SIEM configuration
•	Log analysis
•	Security monitoring
•	Incident detection
•	Authentication event investigation

Key Learnings
•	Understanding Windows authentication logs
•	Identifying brute-force attack indicators
•	SIEM search and filtering techniques
•	Basic SOC monitoring workflow

Status
•	Completed ✅

________________________________________

Week 2 – Vulnerability Assessment
Malware Detection – Endpoint Security + SIEM

Overview
•	Simulate malware activity using a safe test file.
•	Monitor endpoint security alerts.
•	Investigate detection using SIEM logs.

Environment
•	Windows 10 VM
•	VirtualBox
•	Endpoint protection software
•	SIEM platform
•	Malware simulation test file

Attack / Activity Simulation
•	Downloaded malware simulation file.
•	Triggered endpoint protection alert.
•	Verified detection in Windows Event Viewer (Event ID 1116).

Detection / Analysis Endpoint Detection
•	Antivirus identified file as malicious.
•	Generated security alert in system logs.

SIEM Analysis
•	Ingested endpoint security logs.
•	Resolved log permission issues.
•	Investigated malware detection events.

Search Queries:
•	index=* EventCode=1116
•	index=* "Windows Defender"

Findings
•	Malware simulation successfully detected.
•	Alert visibility confirmed in SIEM.
•	Verified proper log ingestion and monitoring.

Skills Demonstrated
•	Endpoint monitoring
•	Log ingestion and troubleshooting
•	Malware alert investigation
•	Incident response workflow
•	Security event correlation

Key Learnings
•	How antivirus detection works
•	Onboarding endpoint logs to SIEM
•	Managing Windows permissions
•	Investigating malware alerts in SOC workflow
•	Incident documentation practices

Status
•	Completed ✅

________________________________________

Week 3 – Incident Response Simulation
Network Traffic Analysis – Packet Monitoring + SIEM

Overview
•	Capture and analyze network traffic.
•	Identify suspicious communication patterns.
•	Perform network-based incident investigation.

Environment
•	Kali Linux VM
•	Windows 10 VM
•	VirtualBox
•	Network packet analyzer
•	SIEM platform

Attack / Activity Simulation
•	Generated network activity between virtual machines.
•	Captured packets during communication.
•	Exported captured traffic as PCAP files.

Detection / Analysis Packet Analysis
•	Inspected captured network packets.
•	Applied filters to identify unusual activity.
•	Observed abnormal connections and protocols.

SIEM Analysis
•	Imported network traffic logs.
•	Correlated packet data with system activity.

Search Queries:
•	index=*
•	sourcetype=pcap

Findings
•	Identified suspicious network behavior.
•	Detected unusual connection attempts.
•	Correlated network traffic with potential threats.

Skills Demonstrated
•	Network traffic monitoring
•	Packet inspection
•	PCAP analysis
•	Log correlation
•	Incident investigation
•	SOC network analysis

Key Learnings
•	Understanding packet-level investigations
•	Detecting abnormal network behavior
•	Using filters for traffic analysis
•	Integrating network data into SIEM
•	Real-world SOC investigation process

Status

Completed ✅


### Week 4 – Threat Hunting (MITRE ATT&CK)
Status: Planned


Maintained by: Sai Naga Sabarish Yerramsetty
