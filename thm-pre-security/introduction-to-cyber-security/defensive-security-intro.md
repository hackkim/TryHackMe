# 🛡️ Introduction to Defensive Security

> “While offensive security breaks, defensive security protects.”

In the previous room, we explored offensive security — the practice of identifying and exploiting system vulnerabilities to strengthen defenses. This included exploiting software bugs, abusing weak configurations, and bypassing access control. Red teams and penetration testers specialize in these techniques.

Now, we shift focus to the other side: **Defensive Security**.

---

## 🧠 Task 1: What is Defensive Security?

Defensive Security focuses on:

- ✅ Preventing cyber intrusions  
- ✅ Detecting and responding to threats in real time

![Defensive Security Overview](https://github.com/user-attachments/assets/258c170c-317e-4bbe-b850-25289b38c326)

The teams responsible for this are known as **Blue Teams**.

---

### 🔧 Common Defensive Security Tasks

- **Cyber Security Awareness Training** – Teaching users to recognize and prevent common attacks.
- **Asset Management** – Keeping track of all systems and devices that require protection.
- **Patching Systems** – Regularly updating software and hardware to eliminate vulnerabilities.
- **Firewalls & IPS** – Controlling traffic and blocking known threats using firewalls and Intrusion Prevention Systems.
- **Logging & Monitoring** – Setting up logging systems to detect unusual or malicious activity, such as unauthorized devices joining the network.

> Defensive security doesn’t stop there — it also includes deep analysis and response capabilities like SOC, Threat Intelligence, DFIR, and Malware Analysis.

---

## 🧩 Task 2: Key Areas of Defensive Security

This section explores two main areas of defensive security:

- **Security Operations Center (SOC)** + Threat Intelligence  
- **Digital Forensics and Incident Response (DFIR)** + Malware Analysis

---

### 🖥️ Security Operations Center (SOC)

A **SOC** is a team of cybersecurity professionals that monitor networks and systems to detect malicious activity.

![SOC Operations Center](https://github.com/user-attachments/assets/08badee5-b1c1-401a-8897-595b13de97e1)

#### Focus Areas:

- **Vulnerabilities** – Applying patches or mitigations to prevent exploitation.
- **Policy Violations** – Detecting violations like uploading sensitive data to external services.
- **Unauthorized Activity** – Recognizing compromised user accounts and preventing misuse.
- **Network Intrusions** – Identifying and reacting to threats like malware or phishing.

---

### 🧠 Threat Intelligence

Threat Intelligence involves gathering and analyzing data on threats and attackers.

- **Threats** are any actions that harm a system.
- **Adversaries** range from nation-state attackers to criminal ransomware groups.

#### Intelligence Lifecycle:

1. **Collect** – From internal logs, forums, dark web, and threat feeds.
2. **Process** – Organize data into readable, structured formats.
3. **Analyze** – Discover attacker patterns and motives.
4. **Respond** – Take informed actions to mitigate or prevent future attacks.

> Outcome: A **threat-informed defense** capable of anticipating future attacks.

---

## 🔍 DFIR: Digital Forensics & Incident Response

### 🧪 Digital Forensics

Forensics applies science to uncover evidence of cybercrimes.

#### Areas of Focus:

- **File Systems** – Analyze deleted, modified, or hidden files.
- **System Memory** – Investigate malware running only in memory.
- **System Logs** – Examine login history, command executions, etc.
- **Network Logs** – Review traffic history for suspicious behavior.

---

### 🚨 Incident Response

Incident Response defines how an organization reacts to a cyberattack or breach.

#### 4 Phases of Incident Response:

1. **Preparation** – Build a trained team and preventive infrastructure.
2. **Detection & Analysis** – Identify and assess the incident.
3. **Containment, Eradication, Recovery** – Stop, remove, and fix the threat.
4. **Post-Incident** – Document findings and lessons learned.

![Incident Response Lifecycle](https://github.com/user-attachments/assets/17a44869-19c1-404c-a29f-d7f08f06b905)

---

### 🐛 Malware Analysis

Malware = Malicious + Software. Common types include:

...

![Malware Analysis Visual](https://github.com/user-attachments/assets/fe370002-c962-4adb-921c-a984f223dcca)

- **Virus** – Self-replicating code that corrupts systems.
- **Trojan Horse** – Disguised as legitimate software with hidden malicious behavior.
- **Ransomware** – Encrypts files and demands ransom for decryption.

![Firewall and Network Filtering](https://github.com/user-attachments/assets/7069acf2-50c7-419f-9d1b-14458aca0ba9)

#### Malware Analysis Techniques:

1. **Static Analysis** – Reviewing code without executing it (requires assembly knowledge).
2. **Dynamic Analysis** – Running the malware in a sandboxed environment to observe its behavior.

---

## 🧪 Task 3: Practical Example of Defensive Security

### Scenario: You're a SOC Analyst

You're tasked with protecting a bank using a **Security Information and Event Management (SIEM)** system. It collects logs and security alerts from all systems.

You receive alerts such as:

- ❌ Multiple failed login attempts  
- ❓ Unknown IP trying to connect  
- ⚠️ Suspicious network behavior

Not every alert is malicious. It’s your job to investigate, analyze, and respond appropriately.

---

### 🕹️ Simulated SIEM Experience

TryHackMe provides a simplified SIEM simulation so you can experience what a real analyst would encounter.

> 🖱 Click the **"View Site"** button in the room to launch the simulation.

Look for the **flag** (`THM{EXAMPLE_FLAG}`) by following clues in the simulated alerts.

---

## 📚 What’s Next?

In this room, you explored:

- The foundations of **Defensive Security**
- Key areas like **SOC, Threat Intelligence, DFIR, and Malware Analysis**
- A hands-on SIEM simulation experience

> 🧠 The world of cyber threats is constantly evolving — defensive security requires continuous learning and adaptation.

---

## 🔗 Suggested Next Rooms on TryHackMe:

- **[Introduction to SIEM](https://tryhackme.com/room/introtosiem)** – Learn the basics of SIEM technology  
- **[Security Operations](https://tryhackme.com/room/securityoperations)** – Explore SOC responsibilities and data sources  
- **[DFIR: An Introduction](https://tryhackme.com/room/dfirintro)** – Get started with digital forensics and incident response  
- **[Intro to Malware Analysis](https://tryhackme.com/room/introtomalwareanalysis)** – Understand how to investigate malicious programs

---

🧠 Stay vigilant. Stay informed. Stay defensive.
