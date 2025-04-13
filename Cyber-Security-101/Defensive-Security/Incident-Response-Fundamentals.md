# 🛡️ TryHackMe: Introduction to Incident Response (Full Summary with Visuals)

This document is a complete visual and structured summary of the TryHackMe room **"Introduction to Incident Response"**, including explanations of core concepts, incident types, frameworks, tools, and practical techniques.

---

## 🧠 Task 1: Introduction to Incident Response

Incident Response (IR) is the structured approach to handle cyber threats — not just to prevent them but to **prepare, respond, recover, and improve**.

Imagine your house has expensive items. You install CCTV and a guard — proactive defense. But what if someone gets in? You still need to react. That’s Incident Response.

![Home Security Analogy](https://github.com/user-attachments/assets/5fab1ee1-69f3-407f-8c72-3cca7e6dbbf0)
![Logs to Alert Pipeline](https://github.com/user-attachments/assets/13fc6658-0f2f-4064-b3d6-157568bdf679)

### Objectives:
- Understand what incidents are
- Learn how to assess their severity
- Explore IR frameworks (SANS/NIST)
- Know the tools and playbooks used
- Perform hands-on phishing incident lab

---

## 🔍 Task 2: What Are Incidents?

Computers run many processes like `explorer.exe` and `svchost.exe`, all of which create **events**. These are analyzed by security solutions.

- **False Positives**: Not harmful but flagged
- **True Positives**: Real threats → become **incidents**

![Event Flow to Security Team](https://github.com/user-attachments/assets/97e61728-1c92-4d33-89ba-f3177a6c397f)
![Incident Classification and Severity Table](https://github.com/user-attachments/assets/dc78f640-c6c5-4ba2-abdd-9e6473f1171a)

### Severity Levels:
- Low, Medium, High, Critical — based on potential impact

---

## 🚨 Task 3: Types of Incidents

Each incident type affects an organization differently:

### 🦠 Malware Infections
Malicious code spreads via files, scripts, attachments.

![Malware Infection](https://github.com/user-attachments/assets/66497696-4c52-469c-be30-8fd4c9013a80)

### 🕵️ Security Breaches
Unauthorized access to systems/data.

![Security Breach](https://github.com/user-attachments/assets/0501358b-7d8a-4796-99ff-e782caff60f0)

### 💧 Data Leaks
Sensitive info exposed, intentionally or accidentally.

![Data Leak](https://github.com/user-attachments/assets/43fcc8f3-65f2-40cc-bac1-63c731737082)


### 🧍 Insider Attacks
Employees misusing access.

![Insider Threat](https://github.com/user-attachments/assets/4115a736-1b13-47d8-ac02-64308c27930b)


### 💣 Denial of Service (DoS)
Systems are overwhelmed and shut down by fake requests.

![DoS Attack](https://github.com/user-attachments/assets/4897bad4-5fae-4a86-adc8-2d1ddaf7180b)

---

## 🔁 Task 4: Incident Response Process

To respond efficiently, we use frameworks like **SANS** and **NIST**.

### 🔹 SANS (PICERL)
1. Preparation
2. Identification
3. Containment
4. Eradication
5. Recovery
6. Lessons Learned

![SANS PICERL Cycle](https://github.com/user-attachments/assets/6368adb9-c80c-4428-a19d-5641a5f4acb5)

### 🔸 NIST
1. Preparation
2. Detection and Analysis
3. Containment, Eradication, Recovery
4. Post-Incident Activity

![NIST Flow Model](https://github.com/user-attachments/assets/e2ed0533-bc89-49ce-8134-cf5d41c98f45)


### 📊 Comparison

| SANS                      | NIST                                       |
|---------------------------|--------------------------------------------|
| Preparation               | Preparation                                |
| Identification            | Detection and Analysis                     |
| Containment               | Containment, Eradication, and Recovery     |
| Eradication               |                                            |
| Recovery                  |                                            |
| Lessons Learned           | Post-Incident Activity                     |

![SANS vs NIST Comparison](https://github.com/user-attachments/assets/3936da01-f7ed-439c-bda4-607725220d69)

---

## 🛠️ Task 5: Incident Response Techniques

Organizations use automation to detect/respond faster.

### Tools:

![Security Monitoring Dashboards](https://github.com/user-attachments/assets/0a904e9c-7a62-49d0-a66b-f5976eb465c0)

| Tool | Description |
|------|-------------|
| SIEM | Collects logs, detects threats |
| AV   | Detects malware via signatures |
| EDR  | Endpoint monitoring & response |

---

### 📘 Playbooks vs Runbooks

![Playbook Guide](https://github.com/user-attachments/assets/48d3b333-b040-4cd6-9561-368f2ad14c57)

- **Playbook** = What to do (strategic)
- **Runbook** = How to do it (step-by-step)

#### Example: Phishing Playbook
1. Notify
2. Analyze
3. Inspect attachments
4. Check user impact
5. Isolate
6. Block sender

---

This covers Tasks 1 to 5 with visuals. Tasks 6 and 7 involve the interactive lab and wrap-up.

Stay sharp, stay secure! 🛡️

---

## 🧪 Task 6: Lab Work - Incident Response

In this simulated exercise, you perform a **real-world phishing incident response**.

### 🧾 Scenario:
- A user receives a **phishing email** with a malware attachment.
- Once opened, the file may **infect** the host and **propagate**.
- Your role is to:
  1. Detect the compromised hosts
  2. Identify which systems downloaded vs executed the malware
  3. Contain the affected hosts
  4. Review event timelines
  5. Take appropriate remediation action

> The lab emphasizes detection, isolation, and documentation across multiple affected systems.

---

## ✅ Task 7: Conclusion

### 🧠 Key Takeaways from the Room:

- ✅ How to **identify** an incident using security alerts
- ✅ How to classify incidents by **severity** (Low → Critical)
- ✅ Types of incidents: **malware**, **breaches**, **data leaks**, **DoS**, **insider threats**
- ✅ Frameworks for incident response: **SANS PICERL**, **NIST**
- ✅ Use of tools: **SIEM**, **EDR**, **AV**
- ✅ How to write and use **Playbooks** and **Runbooks**
- ✅ Completed a full **phishing incident response** simulation

---

**Incident Response is not a one-time event — it's a continuous cycle of detection, response, and improvement.**

Stay alert, build strong processes, and never stop learning.

🎯 Room: [TryHackMe - Introduction to Incident Response](https://tryhackme.com)

