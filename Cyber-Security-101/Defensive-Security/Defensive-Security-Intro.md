# 🛡️ TryHackMe - Defensive Security Intro (Highly Detailed Summary)

This document summarizes the **Defensive Security Intro** room from TryHackMe in depth. It introduces essential concepts of cyber defense, including Security Operations Centers (SOC), threat intelligence, digital forensics, incident response, and malware analysis.

---

## 🧠 Task 1 - Introduction to Defensive Security

While offensive security focuses on exploiting vulnerabilities, **defensive security** centers around:

1. 🛡️ **Preventing cyber intrusions**
2. 🔍 **Detecting intrusions and responding effectively**

### 🔵 Blue Team Objectives
- Train users to recognize cyber threats
- Maintain detailed asset inventories
- Keep systems patched and up-to-date
- Deploy security appliances (e.g., firewalls, IPS)
- Monitor systems and analyze logs for anomalies

> Defensive security aims to **detect and respond** before damage occurs.

---

## 🔍 Task 2 - Areas of Defensive Security


### 🖼️ Visualizing Defensive Security Components

#### 👩‍💻 SOC Analysts in Action
![SOC Analysts](https://github.com/user-attachments/assets/a39d737e-a363-4e41-a148-e376618906ce)

#### 📊 Data Aggregation via SIEM Funnel
![SIEM Funnel](https://github.com/user-attachments/assets/ed0fc493-b6a4-43cd-8efc-f225e2307daa)

#### 📉 Incident Response Process Flow
![Incident Response Flow](https://github.com/user-attachments/assets/734a57b6-6da0-43ab-bc3a-f7eb1fb0a766)

#### 💀 Malware Reverse Engineering
![Malware Analysis](https://github.com/user-attachments/assets/339d1fa8-ea48-4085-b861-c3c3b9dfd02c)


Defensive security is composed of multiple domains, most notably:

### 🧭 Security Operations Center (SOC)

A **SOC** is a centralized team responsible for:
- Monitoring systems and networks
- Identifying threats and vulnerabilities
- Triage and escalation of alerts
- Coordination during incidents

#### SOC Responsibilities:
| Focus Area         | Description |
|--------------------|-------------|
| Vulnerability Management | Identify and patch weaknesses |
| Policy Enforcement       | Monitor for policy violations |
| Unauthorized Activity    | Detect stolen credentials in use |
| Network Intrusions       | Identify suspicious network access |

---

### 📡 Threat Intelligence

Threat Intelligence = Collecting, processing, and analyzing data about threat actors.

#### Intelligence Workflow:
1. **Collection** – Logs, sensors, open-source feeds
2. **Processing** – Normalize and correlate data
3. **Analysis** – Profile adversaries, motives, and TTPs
4. **Dissemination** – Share findings with decision-makers

#### Why It Matters:
- Predict attacker behavior
- Build **threat-informed defense**
- Tailor security controls based on relevant threats

---

### 🧠 Digital Forensics and Incident Response (DFIR)

DFIR includes both **investigation** and **remediation** processes.

#### 🕵️ Digital Forensics:
Analyze digital artifacts to determine what happened.

| Artifact | Purpose |
|----------|---------|
| File Systems | Recover deleted or modified files |
| Memory Dumps | Analyze running malware not stored on disk |
| System Logs | Audit user activity and system changes |
| Network Logs | Trace attacker ingress/egress points |

#### 🚨 Incident Response:
Structured plan for dealing with incidents like breaches or malware infections.

**4 Phases of IR:**
1. **Preparation** – Train staff, build playbooks, acquire tools
2. **Detection & Analysis** – Monitor alerts and verify incidents
3. **Containment & Eradication** – Isolate infected systems and remove threats
4. **Post-Incident Activity** – Report findings and improve defenses

---

### 🦠 Malware Analysis

Study malicious code to understand its impact and origin.

#### Common Malware Types:
- **Virus** – Attaches to programs and spreads
- **Trojan Horse** – Masquerades as legitimate software
- **Ransomware** – Encrypts files and demands payment

#### Analysis Techniques:
| Type   | Description |
|--------|-------------|
| Static | Analyze code without execution (e.g., strings, disassembly) |
| Dynamic | Observe behavior in sandboxed environment |

---

## 🧪 Task 3 - Practical Example of Defensive Security


### 🖼️ Example of SOC Alerts on a SIEM Screen

![SIEM Alert Examples](https://github.com/user-attachments/assets/deb2c2bf-8f29-43dd-926c-7e86a3d40e6b)


### 🎯 Scenario: You Are a SOC Analyst at a Bank

- You use a **SIEM** (Security Information and Event Management) system.
- It collects logs from endpoints, servers, network devices.
- It correlates events and triggers alerts.

#### Example Alerts You Might Handle:
- 🔑 Multiple failed login attempts
- 🌐 Connection from an unknown IP
- 📤 Data exfiltration or abnormal transfer behavior

### 🧰 Simulation Lab:
TryHackMe provides an **interactive SIEM dashboard simulation**.

- Investigate alerts
- Filter benign vs malicious activity
- Locate a flag (`THM{...}`)

> Hands-on experience is vital for understanding real-world alert triage.

---

## 📘 Final Thoughts and Continued Learning

This room introduced:

- Core functions of blue teams
- Roles within SOCs and how alerts are processed
- The need for proactive **threat intelligence**
- Forensic analysis workflows
- Malware detection and response strategies

> Defensive security is **data-driven**, **process-oriented**, and **continuous**.

---

## 🧭 What to Learn Next?

| Room | Skill |
|------|-------|
| 🔎 **Search Skills** | Perform OSINT investigations |
| 📊 **Intro to SIEM** | Dive deeper into SIEM platforms |
| 🧠 **DFIR: An Introduction** | Practical forensics walkthrough |
| 🔬 **Intro to Malware Analysis** | Analyze threats step-by-step |
| 📍 **Security Operations** | Build enterprise-level SOC skills |

---

## 🔗 External Resources

- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [US-CERT Incident Response Guide](https://www.cisa.gov/)
- [Wazuh SIEM Open Source Platform](https://wazuh.com/)
- [TheHive Project](https://thehive-project.org/) – IR platform
- [Sigma Rules](https://github.com/SigmaHQ/sigma) – SIEM detection patterns

---

Cybersecurity defense is about **proactivity**, **speed**, and **precision**.
Stay curious, stay ready.
