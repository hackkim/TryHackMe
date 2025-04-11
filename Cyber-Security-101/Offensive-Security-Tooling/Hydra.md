# 🐍 TryHackMe - Hydra (Detailed Room Summary)

This markdown provides an in-depth summary of the **Hydra** room on TryHackMe. This room introduces **THC-Hydra**, a powerful tool used for brute-force password attacks against various services like SSH, FTP, and HTTP login forms.

---

## 📘 Task 1 - Hydra Introduction

### 🔍 What is Hydra?

Hydra is a **parallelized login cracker** designed to perform brute-force attacks against over 50 protocols. It automates password guessing for online services and web applications.

### 🔑 Supported Protocols

Hydra supports a broad range of protocols, including:

- **Network Services**: SSH, FTP, Telnet, RDP, SMB, VNC, SNMP
- **Email Services**: SMTP, POP3, IMAP
- **Databases**: MySQL, PostgreSQL, MSSQL, Oracle
- **Web**: HTTP GET/POST, HTTPS, HTTP-Proxy, HTTP-Form
- **Others**: LDAP, Rlogin, SNMPv1/v2/v3, XMPP, Cisco services

📖 [Official Protocol List](https://github.com/vanhauser-thc/thc-hydra)

---

### 📚 Why Hydra Matters

- Highlights the **importance of strong passwords**
- Common use for **testing weak/default credentials**
- Efficiently automates what would take hours/days manually

**Examples of weak defaults**:
- `admin:admin`
- `admin:password`
- `root:toor`

These are commonly used by:
- IoT devices
- Routers & Cameras
- Out-of-the-box web panels

---

### 💻 Installation & Availability

Hydra comes **pre-installed** on:

- ✅ TryHackMe AttackBox
- ✅ Kali Linux

To install manually:

```bash
# Debian/Ubuntu
sudo apt install hydra

# Fedora/RHEL
sudo dnf install hydra
```

📦 Source code: [THC-Hydra GitHub](https://github.com/vanhauser-thc/thc-hydra)

---

## 🧪 Task 2 - Using Hydra

Once your AttackBox and the target machine are started, access:

```
http://MACHINE_IP
```

⚠️ Wait ~3 minutes after starting the VM.

---

### 🔐 SSH Brute Force

```bash
hydra -l <username> -P <password_list> MACHINE_IP -t 4 ssh
```

#### 📌 Parameters:
| Option | Meaning |
|--------|---------|
| `-l`   | Login name (username) |
| `-P`   | Password wordlist path |
| `-t`   | Threads to use (parallel attempts) |
| `ssh`  | Target protocol |

#### ✅ Example:
```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt 10.10.10.10 -t 4 ssh
```

---

### 🌐 Brute-Forcing Web Login Forms (POST)

Hydra also supports **http-post-form** to brute-force web application login forms.

```bash
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "<path>:<params>:<fail_indicator>" -V
```

#### 🧾 Field Breakdown:
| Element | Description |
|---------|-------------|
| `<path>` | Login page (e.g., `/login`) |
| `<params>` | Login fields (e.g., `username=^USER^&password=^PASS^`) |
| `<fail_indicator>` | Message shown when login **fails** (e.g., `F=incorrect`) |
| `-V` | Verbose mode (log each attempt) |

---

#### ✅ Example:
```bash
hydra -l admin -P rockyou.txt 10.10.10.10 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

- Tries all `rockyou.txt` passwords for user `admin`
- Assumes the login failure message contains `incorrect`
- Web form is located at root `/`

---

## 🧠 Real-World Usage Scenarios

| Scenario | Use Case |
|----------|----------|
| IoT testing | Brute-force routers, cameras, etc. |
| Web apps | Login panels (`admin.php`, `/login`) |
| Red teaming | Initial access, credential reuse |
| Internal pentests | Testing against exposed RDP/SMB |

---

## ⚠️ Ethical Warning

Hydra should **only be used** on systems you are **authorized** to test.

❌ Unauthorized brute-force attacks are illegal and unethical.

---

## 📌 Tips for Effective Use

- Use optimized **wordlists** like `rockyou.txt`, `SecLists`, or custom-made lists.
- Pair with **Burp Suite** to discover login fields/form structures.
- Combine with **Gobuster** to find hidden login pages.

---

## ✅ Summary

| Feature         | Benefit |
|-----------------|---------|
| Fast and parallelized | Speeds up brute-force process |
| Protocol support | Over 50 protocols |
| Flexible | Works for CLI & web |
| Scriptable | Integrates with tools/scripts |

Hydra is a must-have tool in every penetration tester's and bug bounty hunter's toolkit.

---

## 📚 References

- [TryHackMe Hydra Room](https://tryhackme.com/room/hydra)
- [Hydra GitHub](https://github.com/vanhauser-thc/thc-hydra)
- [Hydra Manual Page](https://linux.die.net/man/1/hydra)
- [SecLists Wordlists](https://github.com/danielmiessler/SecLists)
