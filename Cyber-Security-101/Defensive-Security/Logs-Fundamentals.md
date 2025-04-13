# 📘 TryHackMe - Logs Fundamentals (Detailed Summary)

This document provides a **comprehensive breakdown** of the TryHackMe room titled **Logs Fundamentals**. It explains what logs are, their critical role in cybersecurity and investigations, types of logs, how to analyze them, and how they’re applied in real-world digital forensics and incident response.

---

## 🧠 Task 1: Introduction to Logs


### 🧩 What are Logs?

Logs are **digital records** of activity that occur within an operating system, application, or network. They provide visibility into events that have happened on a system.

Logs = **Digital Footprints**  
→ left behind by system operations, user actions, and even cyberattacks.

---

### 🕵️ Analogy: Digital Crime Scene

Just like physical crime scenes rely on traces (e.g., broken doors, CCTV footage, footprints), in cybersecurity, logs are the traces we use to **reconstruct an attack** and identify:
- What happened
- When it happened
- Who did it
- How it was done

![Snowy Cabin Crime Scene](https://github.com/user-attachments/assets/b51cc321-358b-4da9-9dd4-f8d02118e7ff)
![Footprints in the Snow](https://github.com/user-attachments/assets/48f63fc6-2722-49fc-bbe1-2f6afece671b)

---

### 🔍 Why Are Logs Important?

| Use Case | Purpose |
|----------|---------|
| **Security Monitoring** | Detect suspicious activity in real-time |
| **Incident Investigation** | Reconstruct attack paths; conduct root cause analysis |
| **Troubleshooting** | Debugging application/system issues |
| **Performance Monitoring** | Analyze resource usage, system health, and performance bottlenecks |
| **Compliance & Auditing** | Meet legal/regulatory standards with verifiable activity logs |

---

### 🎯 Learning Objectives of the Room:

- Understand different types of logs
- Perform manual log analysis
- Investigate Windows Event Logs
- Investigate Web Access Logs

## 📂 Task 2: Types of Logs

Logs are categorized by **source and function**, allowing analysts to focus only on the most relevant logs for a specific issue or investigation.

![Log Categories and Events](https://github.com/user-attachments/assets/2ba435c5-75f1-4377-9606-e079f7dadb3a)

### 🧾 Log Types:

| Type             | Description                                                                                 | Examples                                                                 |
|------------------|---------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| **System Logs**   | Related to OS activities and status                                                         | Boot logs, driver errors, system crashes                                 |
| **Security Logs** | Track authentication, access control, account changes                                       | Login attempts, user creation, password changes                          |
| **Application Logs** | Activity specific to a software application                                                 | Crash reports, usage tracking, configuration changes                     |
| **Audit Logs**    | Capture data access, policy enforcement, system changes — crucial for compliance            | File access logs, admin commands, configuration changes                  |
| **Network Logs**  | Record inbound/outbound network traffic and firewall activity                               | DNS queries, TCP connections, blocked requests                           |
| **Access Logs**   | Document access to digital resources like websites, databases, and APIs                     | Webserver logs, API request logs, remote access logs                     |

> 🔍 Depending on the system and services, other specialized log types may also exist (e.g., email server logs, DNS logs, proxy logs).

## 🪟 Task 3: Windows Event Log Analysis


Windows OS has a built-in tool called **Event Viewer** to access and analyze system-generated logs.

### 📚 Key Windows Log Categories:

| Category      | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| **Application** | Logs from user applications (e.g., errors, updates)                         |
| **System**      | OS-level messages (e.g., services starting, hardware issues)                |
| **Security**    | Records security events (e.g., logins, account management)                  |

![Windows Event Viewer - Overview](https://github.com/user-attachments/assets/e785c614-b8ef-497d-bdac-74c643562b20)

---

### 📌 Important Event Fields:

- **Log Name** – Which log file this entry belongs to  
- **Event ID** – Unique identifier for the type of event  
- **Time Logged** – Timestamp of the event  
- **Description** – Human-readable summary of what happened

---

### 🔐 Critical Event IDs:

| ID    | Description                                 |
|-------|---------------------------------------------|
| 4624  | Successful login                            |
| 4625  | Failed login                                |
| 4634  | Logoff event                                |
| 4720  | Account created                             |
| 4724  | Password reset attempt                      |
| 4722  | Account enabled                             |
| 4725  | Account disabled                            |
| 4726  | Account deleted                             |

> Use “Filter Current Log” to view only specific Event IDs such as 4624 (logins).

![Event Viewer Log List](https://github.com/user-attachments/assets/2e331c32-0664-45b3-bbfe-d3722b79a725)
![Detailed Logoff Event (4634)](https://github.com/user-attachments/assets/8361e615-6b0e-4dba-addb-b3f41453c00e)
![Using Filter Current Log](https://github.com/user-attachments/assets/0a814c7d-c9b3-4f3f-9359-6c117f12d1c7)
![Filter by Event ID](https://github.com/user-attachments/assets/1a5c4034-3409-4e2e-b086-27ce5716cd47)
![Filtered Results](https://github.com/user-attachments/assets/5bf1c56b-1a82-4889-acfb-7d8710510a7e)

---

### 🧪 Investigation Scenario:

An attacker exfiltrated data from a file server. Your job:
- Log into the compromised system (via RDP or GUI)
- Use Event Viewer to track the attacker’s activities
- Focus on **4624**, **4720**, etc. for login/account events

![Investigation Credentials](https://github.com/user-attachments/assets/125c569b-1e91-415f-9b57-ebcd9b03cd91)

```
Username: Administrator
Password: logs@123
IP Address: MACHINE_IP
```
## 🌐 Task 4: Web Server Access Log Analysis

Web servers (like Apache, Nginx) generate **access logs** for every request received.

### 📄 Log Entry Sample:
```
192.168.1.1 - - [06/Jun/2024:13:56:44] "GET /about HTTP/1.1" 200 "-" "Mozilla/5.0 ..."
```

### 📌 Key Fields:
- **IP Address** – Who made the request
- **Timestamp** – When request occurred
- **HTTP Method** – GET, POST, PUT, DELETE
- **URL** – Requested resource
- **Status Code** – 200 OK, 404 Not Found, 500 Server Error
- **User-Agent** – Info about the user’s OS and browser

---

### 🔍 CLI Tools for Log Analysis (Linux):

| Command | Purpose |
|---------|---------|
| `cat`   | Print log file contents |
| `grep`  | Search logs for patterns (e.g., IPs, URLs) |
| `less`  | Paginate logs for easier browsing |
| `cat file1 file2 > combined.log` | Merge log files |

---

### 🔧 Example Commands:

```bash
# View full log
cat access.log

# Search for a specific IP
grep "192.168.1.1" access.log

# Combine multiple log files
cat access1.log access2.log > combined_access.log

# Browse logs interactively
less access.log
# In less, use /keyword, then n/N to navigate
```

> File Location (on AttackBox): `/root/Rooms/logs/access.log`

> ⚠️ Some browsers may flag log files as suspicious when downloaded — override with “Keep File” if needed.

---

## ✅ Task 5: Conclusion

Logs are a **vital source of evidence** in security operations.

### 🧾 In This Room You Learned:
- What logs are and how they’re used in forensics and compliance
- Types of logs: system, security, audit, application, network, and access
- How to analyze logs manually on Windows (Event Viewer)
- How to parse and extract data from web access logs using Linux commands

> Mastering logs = Mastering visibility  
> Without logs, you’re blind in security.

---

🎯 [TryHackMe Room: Logs Fundamentals](https://tryhackme.com/room/logsfundamentals)
