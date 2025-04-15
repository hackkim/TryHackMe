# 🔍 TryHackMe - CAPA: The Basics

> CAPA (Common Analysis Platform for Artifacts) is a powerful static analysis tool developed by Mandiant (formerly FireEye).  
> It allows analysts to detect the capabilities of a binary by matching patterns and rules against known behaviors.

---

## 🧠 Task 1 - Introduction


![Static Malware Analysis Concept](https://github.com/user-attachments/assets/853432f8-dae7-4970-95f9-1af7f36d763f)

![CAPA VM Credentials](https://github.com/user-attachments/assets/1010895e-e4a7-4602-ae47-a754ab734ada)


CAPA enables analysts to understand **what a binary can do** without executing it. This is known as **static analysis**.

### 🧱 Dynamic vs Static Analysis

- **Dynamic Analysis**: Observes behavior during execution (risk of infection)
- **Static Analysis**: Reviews code and binary structure without execution (safe)

### 🔧 What CAPA Analyzes

- PE (Portable Executables)
- .NET binaries
- ELF (Linux) files
- Shellcode
- Sandbox reports

### 🎯 Learning Objectives

- Understand what CAPA is and what it detects
- Navigate and interpret output from CAPA
- Recognize common capabilities and mapping standards
- Use Web Explorer and verbose results for in-depth insight

---

## ⚙️ Task 2 - How CAPA Works

### 📁 Setup

Pre-installed on the TryHackMe VM at:
```
C:\Users\Administrator\Desktop\capa
```

Preprocessed files:
- `cryptbot.bin`
- `cryptbot.txt`
- `cryptbot_vv.txt`
- `cryptbot_vv.json`

### 🖥️ Running CAPA

Basic usage:

```powershell
capa.exe .\cryptbot.bin
```

Verbose output:

```powershell
capa.exe -v .\cryptbot.bin
capa.exe -vv .\cryptbot.bin
```

JSON output (for Web Explorer):

```powershell
capa.exe -vv -j .\cryptbot.bin > cryptbot_vv.json
```

> ⚠️ Verbose scanning may take several minutes.

---

### 📋 Sample Output Sections

- File hashes: MD5, SHA1, SHA256
- Platform: OS, architecture, PE format
- Mappings: MITRE ATT&CK, MAEC, MBC
- Capabilities and Namespaces

---

## 🧩 Task 3 - General Info, MITRE & MAEC

### 📑 Metadata Fields

| Field     | Description                          |
|-----------|--------------------------------------|
| MD5       | File hash                            |
| SHA1      | Secondary hash                       |
| SHA256    | Most secure hash                     |
| Format    | File type (PE, ELF, etc.)            |
| OS        | Target operating system              |
| Arch      | Architecture (x86, x64, etc.)        |

---

### 🧠 MITRE ATT&CK Mapping

CAPA maps behaviors to **ATT&CK tactics and techniques**:

Example:

| Tactic          | Technique                                      |
|------------------|------------------------------------------------|
| Defense Evasion | Obfuscated Files (T1027, T1027.005)            |
| Execution       | PowerShell Execution (T1059.001)               |
| Persistence     | Scheduled Tasks (T1053.002, T1053.005)         |
| Discovery       | File Discovery (T1083)                         |

---

### 🧬 MAEC Mapping

**MAEC (Malware Attribute Enumeration and Characterization)** provides a label describing malware function.

| MAEC Category | Description                        |
|----------------|------------------------------------|
| Launcher       | Behavior resembling execution, C2, persistence |
| Downloader     | Downloads and runs additional payloads         |

---

## 🧠 Task 4 - Malware Behavior Catalogue (MBC)

**MBC** describes malware’s behavior using structured attributes.

### 🔍 Format Types

- `OBJECTIVE::Behavior::Method [ID]`
- `OBJECTIVE::Behavior [ID]`

### 🧠 Objective Examples

| Objective              | Description                                            |
|------------------------|--------------------------------------------------------|
| Anti-Behavioral        | Evasion of sandbox/debugging                           |
| Anti-Static Analysis   | Obfuscation, stack strings                             |
| Discovery              | System & file enumeration                              |
| Execution              | Runs scripts, programs, or interpreters                |
| Data                   | String manipulation, encoding                          |

---

### 🔬 Micro-Objectives & Micro-Behaviors

| Micro-Objective | Micro-Behavior        | ID        |
|------------------|------------------------|-----------|
| MEMORY           | Allocate Memory        | C0007     |
| PROCESS          | Create Process         | C0017     |
| DATA             | Encode Base64          | C0026.001 |
| FILE SYSTEM      | Write File             | C0052     |

---

## 🧠 Task 5 - Understanding Namespaces

![CAPA Namespace Structure](https://github.com/user-attachments/assets/db932abd-75d0-4a52-b3b7-51a80b44510f)

Namespaces organize CAPA rules under **top-level categories (TLNs)**.

### 🧩 Format

```
<Capability>::<Top-Level Namespace>/<Sub-Namespace>
```

Example:

```
reference Base64 string::data-manipulation/encoding/base64
```

---

### 🗂 Common TLNs and Purpose

| TLN              | Description                               |
|------------------|--------------------------------------------|
| anti-analysis    | Obfuscation, packing, anti-debugging       |
| communication    | HTTP, DNS, FTP, C2                         |
| data-manipulation| XOR, Base64, compression                   |
| persistence      | Registry, scheduled tasks                  |
| host-interaction | File and process interaction               |
| impact           | Effects like C2, sabotage, theft           |
| linking          | Runtime linking, library detection         |
| load-code        | Runtime code execution, PE parsing         |
| nursery          | Experimental or under-review rules         |

---

## 🔍 Task 6 - Understanding Capability

Each **Capability** maps directly to a `.yml` rule file in the rules repo.

### 🧪 Example

- Capability: `reference Base64 string`
- Namespace: `data-manipulation/encoding/base64`
- YML File: `reference-base64-string.yml`

### ⚠️ Exception Handling

- Some capabilities may be found in the **nursery** namespace, not their expected TLN.

---

## 🌐 Task 7 - Very Verbose Output & CAPA Web Explorer


![CAPA Explorer Web Tab](https://github.com/user-attachments/assets/579dcf17-aa6d-4c06-a54b-e386079a8fee)

![CAPA Explorer Home](https://github.com/user-attachments/assets/9e4e45ea-14b7-4ce9-80fe-e1a16c1776ac)

![CAPA Report Table View](https://github.com/user-attachments/assets/11f85786-061c-4632-8d3c-98657475913c)

![Rule Match - VMware](https://github.com/user-attachments/assets/9ca022dc-6ad4-4b1f-957d-45a1634ea5e5)

![Rule Match - schtasks](https://github.com/user-attachments/assets/89b870cc-6958-43ba-b271-e6a4b8712d16)

![Global Search Result - task via at](https://github.com/user-attachments/assets/2cba5e8c-f5cf-41f0-9240-534a3a0ae14d)


### 🔍 Enable `-vv` Output

```powershell
capa.exe -vv .\cryptbot.bin
```

Export as JSON for UI analysis:

```powershell
capa.exe -vv -j .\cryptbot.bin > cryptbot_vv.json
```

---

### 🌐 Using CAPA Web Explorer

1. Open `capa_web_explorer_offline.html` from Desktop
2. Click `Upload from local`
3. Select `cryptbot_vv.json`
4. Click on rules to:
   - View matched strings (e.g., `/VMWare/i`)
   - Explore rule logic and regex
   - Visualize matching conditions

---

### 🧭 Bonus Features

- Global search box
- Filtering by capability, string, or rule
- Quick trace of how behaviors were detected

---

## ✅ Task 8 - Conclusion

### 🚀 What You've Learned

- Run CAPA against PE or ELF binaries
- Interpret output: MITRE ATT&CK, MAEC, MBC
- Understand Capabilities, Namespaces, Rule mapping
- Use `-v`, `-vv`, `-j` for custom output
- Explore with CAPA Web Explorer

### 🧠 When to Use CAPA

- Initial triage of suspicious files
- Quick capability discovery
- Mapping to ATT&CK techniques in reports
- Signature-based static detection in sandboxes

---

## 📚 Further Resources

- [CAPA GitHub](https://github.com/mandiant/capa)
- [CAPA Rules](https://github.com/mandiant/capa-rules)
- [CAPA Web Explorer](https://github.com/mandiant/capa-explorer)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [MBC Documentation](https://mbcproject.github.io/)
- [MAEC Language](https://maecproject.github.io/)
