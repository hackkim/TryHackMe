# 🔐 TryHackMe: Privilege Escalation Path Overview

This learning path is designed to teach the essential techniques and tools used in **Privilege Escalation**, an important phase in penetration testing. The path covers both **Linux** and **Windows** privilege escalation scenarios, including how to gain reverse/bind shells as a prerequisite to escalating access.

---

## 🧭 Path Overview

![Privilege Escalation Overview](https://github.com/user-attachments/assets/f3d85713-2f58-41f9-a1a8-2bb1c58b1fcd)

**Privilege Escalation**  
Gain access to techniques that allow elevation of account privileges in both Linux and Windows systems. Escalating privileges helps attackers move from a limited shell to full administrative access, essential for system compromise and post-exploitation activities.

---

## 1️⃣ What the Shell?

![What the Shell?](https://github.com/user-attachments/assets/fdadd697-eaf1-4418-bae2-bcfde7b23b2a)

- **Goal**: Understand reverse and bind shell fundamentals used to interact with compromised machines.
- **Topics Covered**:
  - Reverse Shells: Target connects back to attacker
  - Bind Shells: Attacker connects to the target’s open port
  - Shell behavior in different OS environments
- **Why It Matters**: Shell access is the first step before attempting privilege escalation.

✅ *Module Completed*

---

## 2️⃣ Linux Privilege Escalation

![Linux Privilege Escalation](https://github.com/user-attachments/assets/4850a322-f3c3-46dc-a331-6a3417626a19)

- **Goal**: Learn techniques to escalate from a low-privileged Linux user to root.
- **Topics Covered**:
  - Enumerating system information and misconfigurations
  - Exploiting SUID/SGID binaries and weak permissions
  - PATH variable manipulation
  - Scheduled jobs and cron jobs abuse
  - Kernel exploit execution
  - Capabilities and NFS share vulnerabilities
- **Hands-On**: Practice with over 8 real-world techniques in a simulated lab.

🟢 *Module In Progress*

---

## 3️⃣ Windows Privilege Escalation

![Windows Privilege Escalation](https://github.com/user-attachments/assets/d0a542b3-513a-4519-b648-6eee1ea912c1)

- **Goal**: Understand and exploit privilege escalation vectors in Windows environments.
- **Topics Covered**:
  - Local enumeration with built-in commands (`whoami`, `systeminfo`, etc.)
  - Service misconfigurations
  - Token impersonation and UAC bypass
  - Exploiting AlwaysInstallElevated policy
  - DLL hijacking and unquoted service paths
- **Tools Used**: `WinPEAS`, `Seatbelt`, and manual methods

✅ *Module Completed*

---

## 🧠 Why Privilege Escalation Matters

Privilege escalation enables:
- Full control over a compromised machine
- Ability to disable security features and extract sensitive data
- Lateral movement within a network
- Establishing persistence for long-term access

Learning these techniques strengthens both offensive and defensive cybersecurity skills.

