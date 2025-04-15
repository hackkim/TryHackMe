# 🔐 TryHackMe - Introduction to SIEM

> This documentation provides an in-depth explanation of Security Information and Event Management (SIEM) based on the TryHackMe “Introduction to SIEM” room.

---

## 🧠 Task 1 - Introduction

### 🔍 What is SIEM?

**SIEM** stands for **Security Information and Event Management**. It is a centralized platform that collects, normalizes, stores, and analyzes security-related data from across an organization’s IT infrastructure.

### 🧰 Key Functions of SIEM:

- **Log Collection:** Gather data from various sources including endpoints, servers, network devices, and cloud services.
- **Normalization:** Convert data into a common format.
- **Correlation:** Identify relationships between events from multiple sources.
- **Alerting:** Notify analysts of suspicious or malicious activity.
- **Visualization & Reporting:** Dashboards for monitoring and compliance.

---

## 🎯 Learning Objectives

- Understand what SIEM is and how it works
- Learn the significance of network visibility
- Identify different types of log sources
- Learn how logs are ingested and analyzed
- Explore SIEM capabilities such as correlation and alerting

---

## 🌐 Task 2 - Network Visibility through SIEM

### 🧭 Why is Network Visibility Important?

Understanding every activity within a network helps detect:

- Unauthorized access
- Malware activity
- Data exfiltration
- Misconfigurations

![Network Topology Overview](https://github.com/user-attachments/assets/aa226c11-01f7-492a-84a0-286cf214e3bf)

### 🧱 Example Network Components:

- Windows/Linux endpoints
- Data servers
- Routers
- Web services

Each of these components generates **logs**, which can be:

### 🖥️ Host-Centric Log Sources:

These logs reflect activity within individual systems.

- **Windows Event Logs** – e.g., logon attempts, file access
- **Sysmon** – detailed monitoring (process creation, network connections)
- **Osquery** – real-time endpoint querying

#### Host-Centric Log Examples:
- A file is accessed by a user
- Authentication attempts (successful/failed)
- Registry modification
- PowerShell script execution

### 🌐 Network-Centric Log Sources:

These logs reflect communication over the network.

- **Protocols:** SSH, VPN, HTTP/S, FTP
- **Logs:** Connection attempts, web requests, remote access activity

#### Network-Centric Log Examples:
- SSH login to a remote server
- FTP file transfers
- VPN access to internal resources
- HTTP GET/POST requests

---

### ✅ Importance of SIEM

SIEM helps address log overload by:

- Ingesting logs from multiple sources
- Correlating events
- Detecting threats in real time
- Visualizing data
- Enabling investigations and quick responses

![SIEM Functional Cycle](https://github.com/user-attachments/assets/ee02f7f3-a081-4abc-bc5b-4a20123b4c4f)

---

## 📥 Task 3 - Log Sources and Log Ingestion

### 🪟 Windows Machines:

- Use the **Event Viewer** for log inspection.
- Event IDs categorize logs:
  - **4624** – Successful login
  - **4625** – Failed login
  - **4688** – Process creation

![Windows Event Viewer](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e8dd9a4a45e18443162feab/room-content/30beed26fc514cb7f52773b88a4510b9.gif)

### 🐧 Linux Workstations:

Linux stores logs in:

- `/var/log/httpd/` – Apache access/error logs
- `/var/log/auth.log` or `/var/log/secure` – Authentication logs
- `/var/log/cron` – Scheduled tasks
- `/var/log/kern` – Kernel messages

Sample cron log:
```
May 28 13:04:20 crond[2843]: no timestamp found (user root job sys-daily)
```

### 🌐 Web Servers:

Web servers generate access logs:

```
192.168.21.200 - - [21/Mar/2022:10:17:10] "GET /cgi-bin/try HTTP/1.0" 200 3395
```

---

### 🔗 Log Ingestion Methods:

![Log Ingestion into SIEM](https://github.com/user-attachments/assets/c046fbed-75d3-40a7-9bd0-36b590eb75bd)

1. **Agent/Forwarder:** Installed on endpoints, sends data in real-time to SIEM

2. **Syslog:** Used by Linux systems, firewalls, and routers to transmit logs

![Splunk Data Input Methods](https://github.com/user-attachments/assets/b8155d9d-a624-49cb-b23c-c535fca5a818)

3. **Manual Upload:** For offline logs and quick forensic analysis

4. **Port-Forwarding:** Endpoint sends logs to a designated SIEM port

---

## ⚙️ Task 4 - Why SIEM?

### 📊 SIEM Capabilities:

- Centralized monitoring of host and network logs
- Correlate events across multiple systems
- Real-time alerts for threats
- Threat hunting and investigation
- Historical data retention for compliance

![SOC Ecosystem Diagram](https://github.com/user-attachments/assets/b4df27d1-64bd-4666-8a47-63a41419ac20)

### 👨‍💻 SOC Analyst Responsibilities:

- Continuous monitoring and investigation of alerts
- Rule tuning to reduce false positives
- Compliance reporting
- Identifying coverage gaps in log sources
- Communicating with system owners

---

## 📊 Task 5 - Analyzing Logs and Alerts

### 🖥️ SIEM Dashboards:

Dashboards present real-time and historical insights:

- Summary of alerts
- Login failures
- Top visited domains
- Triggered correlation rules
- System health notifications

![Default SIEM Dashboard Example](https://github.com/user-attachments/assets/5eae06a1-23b2-461b-a771-e6d93befeb83)

### 📐 Correlation Rules:

Rules help automate threat detection:

#### Examples:

- **Multiple Failed Logins:** Trigger if 5 failed login attempts occur within 10 seconds
- **Login After Failures:** Alert when a successful login follows multiple failures
- **USB Activity Detection:** Alert on USB plug if restricted
- **Data Exfiltration:** Alert on outbound traffic exceeding 25MB

### 🧪 Example Use Cases:

**1. Event Log Cleared (Event ID 104):**

```
IF EventLog = WinEventLog AND EventID = 104
THEN Trigger: Event Log Cleared Alert
```

**2. Execution of 'whoami' (Event ID 4688):**

```
IF EventLog = WinEventLog AND EventID = 4688 AND ProcessName CONTAINS "whoami"
THEN Trigger: Suspicious Command Execution Alert
```

---

## 🕵️‍♂️ Alert Investigation Process:

1. Validate the alert (True/False Positive)
2. Review triggered rules
3. Examine affected events
4. Contact asset owners
5. Isolate systems if needed
6. Block malicious IPs/domains
7. Document and report findings

---

## 🧪 Task 6 - Lab Work

> In the lab, review sample SIEM dashboards and explore:
- Alert metadata
- Associated events
- Rule triggers
- Investigative workflows

---

## ✅ Task 7 - Conclusion

### Key Takeaways:

- SIEM provides centralized security event visibility
- Enables proactive detection, investigation, and response
- Analysts rely on SIEM dashboards and correlation rules
- Well-ingested and normalized logs are critical

---

## 📚 Recommended Next Rooms

- **Jr. SOC Analyst**
- **Splunk101 / Splunk201**
- **InvestigatingWithSplunk**
- **InvestigatingWithELK**
- **Benign**
- **ItsyBitsy**

---
