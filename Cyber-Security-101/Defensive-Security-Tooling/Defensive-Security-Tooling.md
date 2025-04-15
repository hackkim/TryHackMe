# 🛡️ TryHackMe - Defensive Security Tooling

> A comprehensive breakdown of the TryHackMe **Defensive Security Tooling** path.  
> This learning path explores essential tools for malware analysis, reverse engineering, and digital forensics, focusing on CyberChef, CAPA, REMnux, and FlareVM.

---

![Defensive Security Tooling Path](https://github.com/user-attachments/assets/06035b4c-ef46-4147-94a2-ff8b27586b2d)

---

## 📘 Overview

The **Defensive Security Tooling** path provides learners with practical knowledge of core tools used in **incident response**, **malware analysis**, and **reverse engineering**.

### ✳️ Objectives

- Decode and transform data using CyberChef
- Analyze binary capabilities with CAPA
- Explore Linux-based malware tools using REMnux
- Investigate Windows malware with FlareVM

---

## 🔧 Room-by-Room Breakdown

### 🔍 CyberChef: The Basics

![CyberChef Room](https://github.com/user-attachments/assets/38e5facb-617e-4553-b508-89383c244e4e)

- A browser-based tool for performing over 300 operations (decoding, encoding, regex, etc.)
- Often used by analysts to convert encodings, inspect payloads, extract hidden data, etc.
- Requires no setup; runs in-browser and supports drag-and-drop workflows
- Example use cases:
  - Decode Base64, ROT13, Hex
  - Parse JWT tokens
  - Analyze obfuscated scripts

🔗 Official site: [https://gchq.github.io/CyberChef](https://gchq.github.io/CyberChef)

---

### 🧠 CAPA: The Basics

![CAPA Room](https://github.com/user-attachments/assets/d88bacae-dddb-4e1b-83a1-4e3e097a1eb5)

- Developed by Mandiant, CAPA analyzes PE files and identifies behaviors and capabilities
- Based on static analysis, not signature-based scanning
- Works by matching predefined rules written in YAML against patterns in disassembly
- Typical results include capabilities like:
  - Create or modify files
  - Use Windows API
  - Inject into processes
  - Command and control

💡 Ideal for triaging suspicious files quickly before dynamic analysis.

---

### 🐧 REMnux: Getting Started

![REMnux Room](https://github.com/user-attachments/assets/023394a5-2ee8-45cf-b042-b2d3ec240156)

- REMnux is a **Linux distro** tailored for reverse engineering and malware analysis
- Preloaded with:
  - Network monitoring tools (Wireshark, tcpflow)
  - Static analysis tools (radare2, binwalk)
  - Dynamic analysis utilities (strace, ltrace, inetsim)
- Designed to run on bare metal or as a VM (VirtualBox or VMware)

🛠 Common Workflow:
1. Use REMnux to unpack/drop malware
2. Analyze strings, sections, metadata
3. Simulate C2 communication

🔗 [REMnux Documentation](https://docs.remnux.org/)

---

### 🪟 FlareVM: Arsenal of Tools

![FlareVM Room](https://github.com/user-attachments/assets/f01fe2aa-e250-419f-a443-b9d3a3a813a8)

- A **Windows-based malware analysis platform** developed by Mandiant
- Installs via PowerShell and includes tools like:
  - x64dbg, PE Studio, IDA Free
  - Sysinternals Suite
  - YARA, OllyDbg, Ghidra
- Offers a sandboxed environment for:
  - Debugging executables
  - Performing behavioral analysis
  - Tracking registry, process, and file changes

🔥 Especially useful for .NET, PE32, DLL, and document-based threats (macros, VBA, etc.)

---

## 🧩 Tool Comparison Table

| Tool       | Platform | Strengths                          | Use Case                     |
|------------|----------|------------------------------------|------------------------------|
| CyberChef  | Web      | Universal decoder, simple workflow | Obfuscation, encoding, quick inspection |
| CAPA       | Windows/Linux | Static binary capability detection | Malware triage, automated insight |
| REMnux     | Linux    | Lightweight reverse engineering VM | Network analysis, sample unpacking |
| FlareVM    | Windows  | Full reverse engineering suite     | Advanced malware lab & sandboxing |

---

## 🧠 Who Should Learn This Path?

- Security Analysts
- Threat Hunters
- Malware Analysts
- Forensics Specialists
- Blue Teamers

---

## ✅ Outcomes

By the end of this path, you will:

- Efficiently inspect and manipulate encoded data
- Perform static analysis on unknown binaries
- Set up and use professional-grade malware analysis environments
- Identify suspicious behaviors in files using rule-based detection

---

## 🚀 Suggested Next Steps

- Build a portable malware analysis lab using REMnux + FlareVM
- Try analyzing live malware samples in a sandbox
- Learn to write **custom CAPA rules**
- Use CyberChef to parse obfuscated phishing emails
- Integrate FlareVM into your incident response SOP

---

## 📚 References

- [CyberChef Documentation](https://gchq.github.io/CyberChef)
- [CAPA GitHub Repo](https://github.com/mandiant/capa)
- [REMnux Project](https://remnux.org/)
- [FlareVM GitHub](https://github.com/mandiant/flare-vm)
