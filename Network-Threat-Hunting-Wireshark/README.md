# Network Traffic Analysis with Wireshark and Splunk
 
**MITRE ATT&CK:** T1040 - Network Sniffing  
**Tools Used:** Wireshark, Splunk, Kali Linux, Windows 10, VirtualBox  
**Verdict:** Suspicious Traffic Successfully Identified and Correlated  
 
---
 
## What This Project Is
 
I set up two virtual machines, Kali Linux and Windows 10, generated network traffic between them, and captured it using Wireshark. I then analyzed the PCAP files for suspicious communication patterns and correlated the findings in Splunk.
 
This replicates the network investigation workflow a SOC analyst follows when investigating a potential network-based threat or lateral movement event.
 
---
 
## Environment Setup
 
| Field | Value |
|---|---|
| Attacker Machine | Kali Linux VM |
| Target Machine | Windows 10 VM |
| Hypervisor | VirtualBox |
| Capture Tool | Wireshark |
| SIEM | Splunk Enterprise |
 
---
 
## Project Workflow
 
1. Set up Kali Linux and Windows 10 VMs on VirtualBox
2. Generated network activity between the two machines
3. Captured live traffic using Wireshark
4. Exported captured traffic as PCAP files
5. Applied Wireshark filters to isolate suspicious patterns
6. Imported PCAP data into Splunk for correlation
7. Documented findings and suspicious indicators
---
 
## Wireshark Filters Used
 
```
ip.addr == [target IP]
```
```
tcp.flags.syn == 1
```
```
http
```
 
## Splunk Queries Used
 
```
index=*
sourcetype=pcap
```
 
---
 
## Key Findings
 
- Identified abnormal connection attempts between the two machines
- Detected unusual protocols and port activity in the captured traffic
- Applied Wireshark display filters to isolate specific suspicious traffic types
- Correlated packet level data with system activity in Splunk to build a fuller picture of the network behavior
- Confirmed the value of combining packet capture with SIEM analysis for network investigations
---
 
## What I Would Do as a SOC Analyst
 
1. Identify the source and destination of suspicious traffic
2. Check if the traffic matches any known attack signatures
3. Determine if data was exfiltrated during the communication
4. Block the suspicious IP at the firewall
5. Correlate the network activity with endpoint logs in the SIEM
6. Document all findings with timestamps and packet evidence
7. Escalate if lateral movement or data exfiltration is confirmed
---
 
## Skills Used
 
`Network Traffic Monitoring` `Packet Inspection` `PCAP Analysis` `Wireshark Filtering` `Log Correlation` `Splunk` `Incident Investigation` `SOC Network Analysis`
 
---
 
*Part of my SOC Analyst portfolio.*  
*Connect on [LinkedIn](https://www.linkedin.com/in/sabarishy/)*
