# 🛡️ TryHackMe - FlareVM: Arsenal of Tools

> FlareVM is a malware analysis and reverse engineering environment built for Windows.  
> Developed by the Mandiant FLARE team, it contains tools for static/dynamic analysis, memory forensics, debugging, and more.

---

## 🧠 Task 1 - Introduction


![FlareVM Toolbox Overview](https://github.com/user-attachments/assets/dc359fb5-e352-4d4f-be68-4f228d8677cc)

![FlareVM Credentials](https://github.com/user-attachments/assets/07a641d2-17bf-497a-ab88-6182b43e47c0)


FlareVM (Forensics, Logic Analysis, and Reverse Engineering Virtual Machine) provides:

- A fully offline analysis environment
- Dozens of pre-installed tools
- A safe platform to reverse malicious files
- A resource for forensic analysts, incident responders, and malware researchers

### 🎯 Learning Objectives

- Explore key FlareVM tools and categories
- Understand their purpose during malware investigations
- Perform hands-on static and dynamic analysis

> 🔐 **Warning**: The FlareVM contains live malware samples. Do not export, move, or execute outside the sandbox!

---

## 💻 VM Access Instructions

- Click **Start Machine** to begin
- Use RDP if needed with credentials:
  - **Username**: Administrator
  - **Password**: letmein123!
- Navigate to:
  ```
  C:\Users\Administrator\Desktop\Sample
  ```

---

## 🧰 Task 2 - Arsenal of Tools by Category

### 🔍 Reverse Engineering & Debugging

| Tool       | Purpose |
|------------|---------|
| Ghidra     | Open-source reverse engineering framework |
| x64dbg     | Modern debugger for Windows binaries |
| OllyDbg    | Assembly-level analysis |
| Radare2    | Lightweight reverse engineering suite |
| Binary Ninja | Decompiler with API and automation support |
| PEiD       | Detects packers, cryptors, and compilers |

---

### 🛠 Disassemblers & Decompilers

- **CFF Explorer** – PE structure and section viewing
- **Hopper** – Mac/Windows reverse engineering
- **RetDec** – Decompile binary back to C-like format

---

### 📑 Static & Dynamic Analysis Tools

| Tool             | Use Case |
|------------------|----------|
| Process Hacker   | Monitor threads, memory, processes |
| PEview           | Inspect PE headers and sections |
| DIE              | File type, compiler, and obfuscation detection |
| Dependency Walker | DLL and function call dependency mapping |

---

### 🕵️ Forensics & IR Tools

| Tool        | Description |
|-------------|-------------|
| Volatility  | Memory forensics & plugin-based parsing |
| Rekall      | Alternative memory analysis framework |
| FTK Imager  | Acquire disk images and preview file systems |

---

### 🌐 Network Tools

- **Wireshark** – Network traffic packet capture and filtering
- **Netcat** – Read/write raw TCP/UDP streams
- **Nmap** – Scan network ports and services

---

### 📂 File Analysis

- **HxD** / **Hex Fiend** – Hex editing
- **FileInsight** – Analyze file structure at byte-level

---

### ⚙️ Automation & Scripting

- **Python** – Malware scripting or deobfuscation tasks
- **PowerShell Empire** – Post-exploitation framework

---

### 🧪 Sysinternals Suite (Essential for IR)

- **Process Explorer** – View running processes and threads
- **Autoruns** – Discover persistence mechanisms
- **Procmon** – Capture real-time file/registry activity

---

## 🔍 Task 3 - Common Tools for Investigation


![Procmon - lsass.exe ReadFile](https://github.com/user-attachments/assets/a5db87e9-24e6-463a-8274-91d808a432e7)

![Process Explorer - CFF Explorer Trace](https://github.com/user-attachments/assets/72ac07cf-aed2-4e94-b48f-b123db2dcec6)

![HxD - PE Signature and Data Inspector](https://github.com/user-attachments/assets/2151f785-8eed-4336-bd3d-3d3141c7486e)

![CFF Explorer - cryptominer.bin PE Metadata](https://github.com/user-attachments/assets/d2236fb0-40d9-4c29-b83f-17e39684a460)

![Wireshark - TLSv1.2 Packet Inspection](https://github.com/user-attachments/assets/ab789b4b-39a3-445c-a806-3e91adc7b8b6)

![PEStudio - Static PE Metadata Analysis](https://github.com/user-attachments/assets/491833d9-4917-42d7-8a8c-4ded37a8b9c8)


### 🧠 Overview

| Tool          | Function |
|---------------|----------|
| Procmon       | Log file, registry, thread activity |
| Process Explorer | Parent-child process view |
| HxD           | Raw file inspection via hex |
| Wireshark     | Detect C2, DNS leaks, packet anomalies |
| CFF Explorer  | View PE metadata and hashes |
| PEStudio      | Evaluate suspicious imports and entropy |
| FLOSS         | Extract obfuscated strings statically |

---

### 🔎 Tool Details

#### 🧭 Procmon

Used to:
- Track suspicious registry or file access
- Detect behavior of tools like Mimikatz
- Filter logs based on process names or paths

#### 🔧 Process Explorer

Allows:
- Insight into parent-child relationships
- DLL and handle inspection
- Verifying whether malicious binaries are spawned

#### 🧬 HxD

Use to:
- Identify PE headers (`MZ`)
- Search for hardcoded C2 IPs
- View encoding or embedded payloads
- Inspect binary structure

#### 📑 CFF Explorer

Analyze:
- Hash values for VirusTotal lookup
- PE timestamps and build date
- Imported function tables
- Suspicious metadata (foreign language strings)

#### 🌐 Wireshark

Useful for:
- Spotting encrypted C2 channels (TLS/SSL)
- Flagging DNS tunneling or exfiltration
- Isolating suspicious IPs

#### 🧪 PEStudio

Highlights:
- Suspicious imports like `CreateRemoteThread`
- Suspicious language metadata
- Packing or encryption based on entropy
- Blacklisted APIs

#### 🔐 FLOSS

Command:

```powershell
FLOSS.exe .\windows.exe > windows.txt
```

Outputs:
- Stack/tight strings
- Registry keys
- Obfuscated URLs, file paths

---

## 🧪 Task 4 - Hands-On File Analysis


![Sample Directory View - windows.exe](https://github.com/user-attachments/assets/923b91ed-5d38-4292-a592-aca5bf8951c9)

![PEStudio - windows.exe Analysis Overview](https://github.com/user-attachments/assets/63b71358-323e-46af-9144-83780741424f)

![PEStudio - File Metadata (Russian Strings)](https://github.com/user-attachments/assets/1d10b17c-4331-4140-acb8-db4f7b58ba16)

![PEStudio - Suspicious API Imports](https://github.com/user-attachments/assets/3dee572b-02d1-4468-aa81-04b5fa468128)

![FLOSS Output - Cryptographic API Strings](https://github.com/user-attachments/assets/c84daf35-fc7a-48d4-b135-9e254bb0d1fd)

![Process Explorer - cobaltstrike.exe Spawned](https://github.com/user-attachments/assets/4cca906e-d48a-431c-ac22-6f5c0df9382c)

![cobaltstrike.exe TCP/IP Tab - Remote Address](https://github.com/user-attachments/assets/3d2d6da0-fae5-496a-96e7-7c9b686af053)

![Procmon Filter Icon UI](https://github.com/user-attachments/assets/7b1230bb-956c-4f47-83fa-3e0d172b9cdb)

![Procmon Filter Conditions - Process Name: cobalt](https://github.com/user-attachments/assets/38dd9e22-4e75-4a7e-b824-2f1b90457e5a)

![Procmon Network Activity - 47.120.46.210](https://github.com/user-attachments/assets/c2dd9661-d8c9-4aa8-b1e3-5143ea740406)


### 🧩 Target: `windows.exe`

#### Step 1: PEStudio

Key finds:
- Metadata faked to mimic regedit
- Russian-language metadata present
- High entropy (possible obfuscation)
- Suspicious imports: `CryptoStream`, `SetUseShellExecute`

#### Step 2: FLOSS

Command:

```powershell
FLOSS.exe .\windows.exe > windows.txt
```

Findings:
- Static strings matched API usage seen in PEStudio
- No decoded `.NET` strings (known limitation)

---

### 🔎 `cobaltstrike.exe` – Dynamic Analysis

#### Step 3: Process Explorer

- Launch binary
- Use TCP/IP tab to view connections
- Identified destination: `47.120.46.210`

#### Step 4: Procmon

- Apply filter: `Process Name contains cobalt`
- View operations by PID
- Confirmed outbound connection, suspicious access

---

## ✅ Task 5 - Conclusion

### 🧠 Summary

In this room, you learned to:

- Navigate the FlareVM environment
- Use core tools across analysis stages:
  - **PEStudio** for static PE inspection
  - **Wireshark** for traffic capture
  - **Procmon/Procexp** for dynamic process tracking
  - **FLOSS** for deobfuscating strings

You also gained:
- Real-world skills in malware behavior detection
- Comfort working with a secure analysis sandbox

> FlareVM empowers analysts with an all-in-one toolkit to dissect, decode, and defend against advanced malware.

---

## 📚 Additional Resources

- [FlareVM GitHub](https://github.com/mandiant/flare-vm)
- [PEStudio](https://www.winitor.com/)
- [FLOSS](https://github.com/mandiant/floss)
- [Sysinternals Suite](https://docs.microsoft.com/en-us/sysinternals/)
- [Wireshark Docs](https://www.wireshark.org/docs/)
