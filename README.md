# 🛡️ SOC Analyst Project: Alert Triage & Incident Escalation in ServiceNow
A comprehensive SOC Tier-1 simulation demonstrating queue management, alert triage, severity classification, analyst documentation, and escalation protocols using **ServiceNow ITSM/SIR**.
---
## 📌 Project Overview
In an enterprise Security Operations Center (SOC), analysts must rapidly differentiate between high-volume background noise, false positives, and multi-stage targeted cyber attacks. 
This project simulates a full L1 shift triage handling **12 security alerts** across Identity (Okta), Endpoint Detection & Response (EDR), Web Proxy, and Perimeter Firewalls.
### Key Objectives
* Triage and categorize security alerts using standard verdict standards (False Positive, Benign True Positive, True Positive).
* Apply standard SOC analyst note syntax (`What Happened`, `Evidence`, `Verdict`, `Next Action`).
* Correlate disparate events across the queue to identify multi-stage attack chains.
* Execute containment workflows and justify incident escalations to Tier-2 / Incident Response.
---
## 📊 Incident Queue & ServiceNow Setup
<img width="1363" height="541" alt="servicenow-queue png - Copy" src="https://github.com/user-attachments/assets/78f3d914-98bf-4e49-9b41-ac53d7dba9e1" />

---
## 📋 Master Alert Triage & Verdict Sheet

| Alert ID | Alert Summary | Source | Severity | Verdict | Action Taken |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **A01** | User Login Anomaly from RU IP | Okta | High | True Positive | Session Revoked & Escalated to IR |
| **A02** | Malware Hash Detected (Mimikatz) | EDR | Critical | True Positive | Host Isolated & Escalated to IR |
| **A03** | Impossible Travel Detected | Okta | Low | Benign True Positive | Corporate VPN match confirmed; Closed |
| **A04** | Suspicious PowerShell Script Download | Proxy | High | True Positive | Outbound Domain Blocked; Escalated |
| **A05** | Diagnostic Tool Flagged (Procmon) | EDR | Low | False Positive | Known Hash Verified; Rule Tuned |
| **A06** | Multiple Failed VPN Logins | VPN | Low | Benign True Positive | User Typo / MFA Success; Closed |
| **A07** | Encoded Base64 PowerShell Execution | EDR | High | True Positive | Process Killed & Host Flagged |
| **A08** | High Volume Outbound Transfer (4.8GB) | Firewall | Critical | True Positive | C2 IP Blocked; P1 Incident Escalation |
| **A09** | New User Account Created in AD | AD | Low | Benign True Positive | HR Ticket #HR-4412 Verified; Closed |
| **A10** | Admin Login from New Region | Okta | Low | Benign True Positive | Approved Conference Travel; Closed |
| **A11** | Phishing Email Reported | Email Gateway | Medium | True Positive | Phish URL Blocked & Inbox Purged |
| **A12** | Privilege Escalation (Token Manipulation) | EDR | Critical | True Positive | DB Server Isolated; P1 Escalation |

---
## 🔍 Identified Attack Chains
Through event correlation across timestamps, usernames, and endpoints, two coordinated attack paths were separated from background noise:
```text
[Attack Chain 1: Credential Access & Domain Compromise]
Alert 01 (Stolen Credentials Login via Russian IP) 
   └──> Alert 02 (Mimikatz dropped on WORKSTATION-04)
           └──> Alert 12 (SYSTEM token manipulation on DB-PROD-01)
[Attack Chain 2: External Delivery & Exfiltration]
Alert 04 (PowerShell download cradle via browser) 
   └──> Alert 07 (Base64 obfuscated execution on FINANCE-PC-02)
           └──> Alert 08 (4.8 GB outbound C2 exfiltration at 03:00 AM)
```

📝 Analyst Note Examples
​Malicious Escalation (Alert 01)
<img width="1336" height="488" alt="alert01-investigation png" src="https://github.com/user-attachments/assets/c950c956-c7ef-4e81-adce-afcda0f49ea4" />

Benign False Alarm (Alert 06)
<img width="1357" height="488" alt="alert06-benign png" src="https://github.com/user-attachments/assets/80fc4df7-25fc-48cc-8543-a24f74888ffa" />

🛠️ Tools & Technologies

​Ticketing & Incident Management: ServiceNow ITSM

​Telemetry Sources: Okta Identity Logs, EDR Agents, Perimeter Firewalls, Web Proxies

​Frameworks: MITRE ATT&CK, NIST SP 800-61 Rev. 2
