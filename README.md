# Cybersecurity Projects Portfolio

Hands-on cybersecurity projects documenting real investigations, detections, and threat analysis. Each project follows the same workflow a SOC analyst would use on the job.

**Analyst:** Sai Naga Sabarish Yerramsetty  
**Focus Areas:** SOC Operations, Threat Intelligence, Incident Response, Network Analysis, Phishing Forensics  
**Connect:** [LinkedIn](https://www.linkedin.com/in/sai-naga-sabarish-yerramsetty-617013210) | [GitHub](https://github.com/SabarishYerramsetty/cybersecurity-projects)

---

## Projects

### 1. Brute Force Detection
**Folder:** `SIEM-Brute-Force-Detection`  
**Tools:** Windows Event Logs, SIEM  
**MITRE ATT&CK:** T1110 - Brute Force  

Detected brute-force login attempts by analyzing Windows authentication failures. Simulated an attacker performing multiple failed login attempts, ingested Event ID 4625 logs into a SIEM, and identified the attack pattern through log queries.

**Skills:** SIEM configuration, log analysis, authentication event investigation, incident detection

---

### 2. Malware Detection
**Folder:** `Malware-Traffic-Analysis-Lab`  
**Tools:** Windows Defender, Splunk, EICAR Test File  
**MITRE ATT&CK:** T1204 - User Execution  

Simulated malware activity using an EICAR test file, triggered a Windows Defender alert, and investigated the detection event in Splunk. Verified the full detection pipeline from endpoint alert to SIEM visibility.

**Skills:** Endpoint security monitoring, SIEM log ingestion, malware alert investigation, incident response workflow

---

### 3. Network Traffic Analysis
**Folder:** `Network-Threat-Hunting-Wireshark`  
**Tools:** Wireshark, Splunk, Kali Linux, Windows 10 VM  
**MITRE ATT&CK:** T1040 - Network Sniffing  

Captured live network traffic between virtual machines using Wireshark, analyzed PCAP files for suspicious communication patterns, and correlated findings in Splunk. Identified abnormal connection attempts and unusual protocols.

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

Built a structured threat intelligence report from the indicators discovered in the phishing investigation. Enriched each IOC through Shodan, ThreatFox, and URLScan. Discovered the server was still active as of June 2026 with SSH publicly exposed, and that the phishing content was likely served from Amazon S3 buckets. Formatted IOCs in STIX 2.1 and wrote detection rules for the email gateway, firewall, and SIEM.

**Skills:** Threat intelligence, IOC enrichment, Shodan reconnaissance, STIX 2.1, detection rule writing, ThreatFox, URLScan

---

## Skills Across All Projects

| Category | Tools and Techniques |
|---|---|
| SIEM | Splunk, Windows Event Logs, log ingestion, search queries |
| Network Analysis | Wireshark, PCAP analysis, packet filtering, traffic correlation |
| Threat Intelligence | ThreatFox, Shodan, URLScan, AbuseIPDB, VirusTotal, WHOIS |
| Email Forensics | MXToolbox, SPF/DKIM/DMARC analysis, header analysis |
| Frameworks | MITRE ATT&CK, STIX 2.1, TAXII |
| Endpoint Security | Windows Defender, Event ID analysis, malware detection |

---

*All projects include full write-ups, screenshots, and investigation reports.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sai-naga-sabarish-yerramsetty-617013210)*
