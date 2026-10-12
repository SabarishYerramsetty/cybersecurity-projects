# Cybersecurity Projects Portfolio

Hands-on cybersecurity projects documenting real investigations, detections, threat analysis, incident response playbooks, and GRC documentation. Each project follows the same workflow a SOC analyst would use on the job.

**Analyst:** Sai Naga Sabarish Yerramsetty  
**Focus Areas:** SOC Operations, Threat Intelligence, Incident Response, Network Analysis, Phishing Forensics, GRC, Risk Management  
**Connect:** [LinkedIn](https://www.linkedin.com/in/sabarishy/) | [GitHub](https://github.com/SabarishYerramsetty) | [Medium](https://medium.com/@ysabarish369)

---

## Projects

### 1. Brute Force Detection
**Folder:** `SIEM-Brute-Force-Detection`  
**Tools:** Splunk, Windows Event Logs, Windows 10  
**MITRE ATT&CK:** T1110 - Brute Force  

Simulated 500+ brute force login attempts on a Windows machine, generating Event ID 4625 failed login events. Ingested logs into Splunk and wrote SPL queries to detect the attack pattern automatically. Cut manual log review time by approximately 60%.

**Skills:** SIEM configuration, Splunk SPL, log analysis, authentication event investigation, incident detection

---

### 2. Malware Detection
**Folder:** `Malware-Traffic-Analysis-Lab`  
**Tools:** Windows Defender, Splunk, EICAR Test File  
**MITRE ATT&CK:** T1204 - User Execution  

Simulated malware activity using an EICAR test file, triggered a Windows Defender alert generating Event ID 1116, and ingested those logs into Splunk. Identified and resolved log permission issues blocking ingestion. Verified the full detection pipeline from endpoint alert to SIEM visibility.

**Skills:** Endpoint security monitoring, SIEM log ingestion, malware alert investigation, log permission troubleshooting, incident response workflow

---

### 3. Network Traffic Analysis
**Folder:** `Network-Threat-Hunting-Wireshark`  
**Tools:** Wireshark, Splunk, Kali Linux, Windows 10, VirtualBox  
**MITRE ATT&CK:** T1040 - Network Sniffing  

Captured live network traffic between two virtual machines using Wireshark, analyzed PCAP files for suspicious communication patterns, applied Wireshark filters to isolate abnormal connections, and correlated findings in Splunk.

**Skills:** Packet inspection, PCAP analysis, Wireshark filtering, network log correlation, SOC investigation workflow

---

### 4. Phishing Email Forensics
**Folder:** `Phishing-Email-Forensics`  
**Tools:** MXToolbox, AbuseIPDB, VirusTotal, DomainTools WHOIS  
**MITRE ATT&CK:** T1566.001 - Spearphishing via Email  

Conducted a full forensic investigation of a real phishing email impersonating Banco Bradesco, one of Brazil's largest banks. Analyzed raw email headers, traced the originating IP through multiple threat intelligence platforms, and performed WHOIS lookup on the sender domain. All three email authentication checks (SPF, DKIM, DMARC) failed. Confirmed the email originated from a DigitalOcean VPS with no affiliation to Banco Bradesco.

**Skills:** Email header analysis, IP reputation analysis, OSINT, WHOIS lookup, IOC identification, MITRE ATT&CK mapping

---

### 5. IOC Report Writing
**Folder:** `IOC-Report-Phishing-Campaign`  
**Tools:** ThreatFox, Shodan, URLScan, STIX 2.1  
**MITRE ATT&CK:** T1566.001 - Spearphishing via Email  

Built a structured threat intelligence report from the indicators discovered in the phishing investigation. Enriched each IOC through Shodan, ThreatFox, and URLScan. Discovered the attack server was still active three years later with SSH publicly exposed and phishing content being served from Amazon S3 buckets. Formatted IOCs in STIX 2.1 and wrote detection rules for the email gateway, firewall, and SIEM.

**Skills:** Threat intelligence, IOC enrichment, Shodan reconnaissance, STIX 2.1, detection rule writing, ThreatFox, URLScan

---

### 6. SOC Incident Response Playbooks
**Folder:** `SOC-Playbooks`  
**Type:** Incident Response Documentation  
**MITRE ATT&CK:** T1566.001, T1110  

Two standardized incident response playbooks built from real investigations and lab simulations. Each covers the full incident response lifecycle from identification through documentation and includes SIEM detection rules and escalation criteria.

Playbooks included:
- Phishing Email Response Playbook (built from the Banco Bradesco investigation)
- Brute Force Attack Response Playbook (built from the Splunk brute force detection lab)

**Skills:** Incident response, SOC process documentation, playbook development, detection engineering, SIEM rule writing

---

### 7. Disaster Recovery and Business Continuity Plan
**Folder:** `DR-BCP-Healthcare-IT`  
**Type:** GRC Documentation  
**Course:** CYBER 5050 - Disaster Recovery and Business Continuity, University of Central Missouri  
**Instructor:** Dr. Richard Morphy  
**Frameworks:** NIST SP 800-34, HIPAA, ISO 22301  

A full Disaster Recovery and Business Continuity Plan developed for a healthcare IT environment. Covers risk assessment, business impact analysis, emergency response, communication planning, recovery strategies, backup and restoration procedures, and testing. Demonstrates understanding of RTO, RPO, MTD, and BIA in a regulated healthcare context.

**Skills:** Disaster recovery planning, business continuity, risk assessment, BIA, RTO/RPO/MTD, HIPAA compliance, GRC documentation

---

### 8. Security Policies and Standards
**Folder:** `Security-Policies-and-Standards`  
**Type:** GRC Documentation  
**Course:** CYBR 5720 - Cyber Security Policies and Risk Management, University of Central Missouri  
**Instructor:** Dr. Richard Morphy  
**Frameworks:** NIST CSF, ISO 27001, CIS Controls  

A set of enterprise-grade security policies, standards, and procedures covering acceptable use, asset management, logging requirements, and information disposal. Demonstrates the ability to write clear and enforceable governance documentation, a core skill in GRC, IAM, and risk roles.

Documents included: Acceptable Use Policy, Asset Management Policy, Logging Standard, Information Disposal Standard, Logging Procedure, Information Disposal Procedure.

**Skills:** Policy writing, GRC documentation, risk governance, compliance, information security management, ISO 27001, NIST CSF

---

## Skills Across All Projects

| Category | Tools and Techniques |
|---|---|
| SIEM | Splunk SPL, IBM QRadar, Windows Event Logs, log ingestion, search queries |
| Network Analysis | Wireshark, PCAP analysis, packet filtering, traffic correlation |
| Threat Intelligence | ThreatFox, Shodan, URLScan, AbuseIPDB, VirusTotal, WHOIS |
| Email Forensics | MXToolbox, SPF/DKIM/DMARC analysis, header analysis |
| Frameworks | MITRE ATT&CK, STIX 2.1, NIST CSF, NIST SP 800-34, ISO 27001, HIPAA |
| Endpoint Security | Windows Defender, Event ID analysis, malware detection |
| GRC | Policy writing, DR/BCP, risk assessment, BIA, compliance documentation |
| Incident Response | Playbook development, detection engineering, SIEM rule writing |

---

*All projects include full write-ups, screenshots, and investigation reports.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sabarishy/)*
