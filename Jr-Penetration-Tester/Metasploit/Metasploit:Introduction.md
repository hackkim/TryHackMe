# 🧨 Metasploit: Introduction

---

## Task 1: Introduction to Metasploit

Metasploit is a powerful and widely used exploitation framework that supports the full lifecycle of penetration testing, including:

- Information Gathering
- Vulnerability Scanning
- Exploitation
- Post-Exploitation
- Report Generation

### Versions of Metasploit

| Version              | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| **Metasploit Pro**   | A commercial version with a graphical user interface (GUI), offering task automation, reporting, and workflow management. |
| **Metasploit Framework** | The open-source command-line interface (CLI) version used for manual exploitation and scripting. Focus of this module. |

---

## Task 2: Main Components of Metasploit

### Core Concepts

- **Vulnerability**: A software flaw or misconfiguration that can be exploited.
- **Exploit**: Code that leverages a vulnerability to execute an action.
- **Payload**: Code delivered through an exploit, such as a shell or command.

### Module Types

- **Auxiliary**: Scanners, crawlers, fuzzers (e.g., `scanner/smb/smb_version`)
- **Exploits**: Attacks exploiting known vulnerabilities (e.g., EternalBlue)
- **Payloads**:
  - **Singles**: Complete and self-contained payloads
  - **Stagers**: Initial connection handlers
  - **Stages**: Larger functional payloads sent after the stager
- **Encoders**: Obfuscate payloads to evade AV detection
- **Evasion**: Modules to actively avoid antivirus detection
- **NOPs**: Used to pad shellcode (e.g., `0x90` for x86)
- **Post**: Used after exploitation for gathering info, persistence, etc.

---

## Task 3: Msfconsole

Metasploit’s primary CLI interface is `msfconsole`.

### Common Commands

- `help`, `help <command>` – View command info
- `search <term>` – Find modules (CVE, service name, etc.)
- `use <module>` – Load a specific module
- `set`, `unset`, `setg`, `unsetg` – Set/unset local and global parameters
- `show options` – View required/optional parameters
- `run`, `exploit` – Launch the selected module
- `back` – Exit module context
- `sessions`, `sessions -i <id>` – Manage Meterpreter or shell sessions

### Exploit Rankings

Below is the exploit reliability classification system used by Metasploit:

![Exploit Ranking](https://github.com/user-attachments/assets/a57c700b-0a64-4fb0-b425-ccbb9fe0bd6d)

---

## Task 4: Working with Modules

When a module is selected, you must configure the necessary options using `set` or `setg`. Always confirm with `show options`.

### Common Parameters

| Parameter | Description |
|-----------|-------------|
| **RHOSTS** | Target IP address or range |
| **RPORT**  | Target port (e.g., 445 for SMB) |
| **LHOST**  | Local attacker IP |
| **LPORT**  | Listening port on attacker's system |
| **PAYLOAD** | Payload to deliver post-exploit |
| **SESSION** | Used in post-exploitation modules |

### Example: Scanning Multiple Targets

```bash
set RHOSTS file:/root/Desktop/targets.txt
```

The targets file may look like:

```
10.10.14.1
10.10.14.2
10.10.14.3
```

Then launch the module:

```bash
use auxiliary/scanner/smb/smb_ms17_010
run
```

Here’s how it looks in practice:

![Target File with Module](https://github.com/user-attachments/assets/baa70096-bafe-44ff-9bb1-522729316a75)

---

## Task 5: Summary

Metasploit enables penetration testers to:

1. **Search** for and identify relevant exploits.
2. **Customize** modules with appropriate parameters.
3. **Launch** exploits and **maintain sessions** via Meterpreter or shell.
4. **Post-exploit** targets to gather credentials, escalate privileges, and establish persistence.

Once you understand the basic navigation of `msfconsole` and module usage, you can integrate Metasploit into real-world testing workflows confidently.
