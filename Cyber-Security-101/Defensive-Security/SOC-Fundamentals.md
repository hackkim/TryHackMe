# 🧠 TryHackMe - SOC Fundamentals (Highly Detailed Summary)

This markdown serves as a complete and structured summary of the **SOC Fundamentals** room from TryHackMe.  
It covers what a Security Operations Center (SOC) is, its core pillars (People, Process, and Technology), team roles, workflows, and how real-world alerts are triaged.

---

## 📌 Task 1 - Introduction to SOC


### 🖼️ SOC Monitoring Room Visualization

![SOC Monitoring Room](https://github.com/user-attachments/assets/381fed99-6e9f-40fa-9dd8-74228547f2a9)


Modern organizations store sensitive digital data. As threat actors continuously search for vulnerabilities, **real-time monitoring** is vital. Traditional security alone isn't enough.

### 🔐 What is a SOC?

A **Security Operations Center (SOC)** is a centralized team responsible for:

- 24/7 monitoring of network and system security
- Detecting suspicious activity or vulnerabilities
- Initiating or supporting incident response
- Minimizing damage caused by intrusions

> SOCs are crucial for proactive and reactive cyber defense.

---

## 🎯 Task 2 - Purpose and Components


### 🖼️ SOC's Core Mission & Pillars

#### 🔍 Detect and Respond
![SOC Detect and Respond](https://github.com/user-attachments/assets/3767ab17-5ac8-4354-b019-b8a665402e56)

#### 🏛️ The Three Pillars of SOC
![SOC 3 Pillars](https://github.com/user-attachments/assets/538c60ed-59fb-4d11-af43-e2e9243882c3)


The SOC's purpose is defined by **Detection** and **Response**.

### ✅ Detection

| Goal | Example |
|------|---------|
| Identify vulnerabilities | Unpatched Windows systems (e.g., MS17-010) |
| Spot unauthorized activity | Suspicious login from unknown geolocation |
| Recognize policy violations | Sharing confidential files via personal email |
| Catch intrusions | Malware from malicious link or web exploit |

### ✅ Response

- Support containment and eradication
- Perform **root cause analysis**
- Aid incident response and forensics teams

---

### 🧱 SOC Pillars: People, Process, and Technology

- **People**: Human expertise in triaging and threat hunting
- **Process**: Repeatable workflows and standard operating procedures (SOPs)
- **Technology**: Tools like SIEM, EDR, and Firewalls that enable scale

These three elements together define a **mature SOC**.

---

## 👥 Task 3 - People


### 🖼️ SOC Team Role Hierarchy

![SOC Role Chart](https://github.com/user-attachments/assets/ac68fd53-9481-4c5c-bac7-4ca0f402bf14)


Despite automation, people remain essential. Why?

- Tools generate **alert noise** (false positives)
- Human judgment is required for prioritization

### SOC Team Roles:

| Role | Function |
|------|----------|
| **Level 1 Analyst** | Alert triage, basic investigation |
| **Level 2 Analyst** | Correlate data across sources, escalate high severity |
| **Level 3 Analyst** | Threat hunting, major IR support, deep analysis |
| **Security Engineer** | Deploy/configure SIEM, EDR, firewall, etc. |
| **Detection Engineer** | Write/maintain detection logic/rules |
| **SOC Manager** | Manage workflow, liaise with CISO, monitor KPIs |

> In small orgs, one person may fulfill multiple roles.

---

## 🔄 Task 4 - Process


### 🖼️ Alert Triage: 5W Investigation Framework

![5W Alert Triage](https://github.com/user-attachments/assets/afefe877-f677-4e9c-aae8-ce22679507c5)


### 🛎️ Alert Triage: The 5 Ws

Use the following framework to break down alerts:

| W | Example |
|---|---------|
| What? | Malware alert on host `GEORGE-PC` |
| When? | June 5, 2024, 13:20 |
| Where? | `C:\Users\George\Downloads` |
| Who? | User `George` |
| Why? | Downloaded pirated software |

### 📝 Reporting

Escalate alerts with:
- 5W breakdown
- Screenshots/logs
- Recommended next steps

### 🧪 Incident Response

If triaged as critical, escalate to IR:
- Contain the threat
- Analyze artifacts (memory, disk, logs)
- Restore affected systems

---

## 🖥️ Task 5 - Technology

Technology enables scale. Without it, triaging thousands of alerts would be impossible.

### 🔧 Core Security Solutions:

| Tool | Description |
|------|-------------|
| **SIEM** | Aggregates logs, applies rules, alerts analysts |
| **EDR**  | Endpoint visibility, malware detection, automated response |
| **Firewall** | Network border defense, blocks malicious traffic |

### Additional Technologies:

- IDS/IPS (Snort, Suricata)
- SOAR (Automated response, e.g., Cortex, XSOAR)
- Antivirus/EPP
- Threat Intelligence platforms
- XDR (eXtended Detection & Response)

> Tech selection depends on risk profile and resources.

---

## 🧪 Task 6 - Practical Exercise (L1 SOC Analyst Simulation)

### Scenario:

You are a **Level 1 SOC Analyst**. An alert has been triggered:

> Port scanning activity detected

### Your Tools:
- A **SIEM platform** with log access
- Threat notification from VA team

### Your Task:
- Review logs for the alert
- Answer the **5Ws**
- Document findings
- Confirm port scan originated from authorized scanner `10.0.0.8`

### Skills Practiced:
- Alert triage
- Log review
- Evidence gathering
- Escalation and ticketing

---

## ✅ Task 7 - Conclusion

This room introduced you to:
- The **structure and mission** of a SOC
- The **three foundational pillars**: People, Process, and Technology
- The **roles** of analysts and engineers
- Real-life **alert handling and escalation**

You also participated in a **simulated SOC exercise** acting as an L1 analyst.

---

## 📚 Further Learning

| Room | Skill |
|------|-------|
| 🔍 Search Skills | Investigative OSINT techniques |
| 📊 Introduction to SIEM | Deep dive into SIEM capabilities |
| 🧬 DFIR: An Introduction | Forensics and Incident Handling |
| 🚨 Incident Response Fundamentals | Plan and execute IR steps |

---

## 🧠 Summary: SOC Pillar Overview

| Pillar | Contribution |
|--------|--------------|
| People | Analysts, engineers, managers with expertise |
| Process | Workflows: triage, escalation, reporting |
| Technology | Tools: SIEM, EDR, firewall, SOAR |

A well-run SOC empowers organizations to detect, respond, and adapt to cyber threats.

---

> “Prevention is ideal, but detection is a must.” – Gartner
