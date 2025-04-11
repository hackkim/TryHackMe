# 🔐 TryHackMe - Offensive Security Tooling Path (Detailed Overview)

![Offensive Security Tooling Banner](https://github.com/user-attachments/assets/b22fd9cd-641a-4c0f-8db6-094ef79c9a20)

> This document provides a comprehensive summary of the **Offensive Security Tooling** path on TryHackMe. This learning path is focused on core offensive tools that penetration testers and red teamers use in real-world scenarios: **Hydra**, **Gobuster**, and **SQLMap**. It also provides foundational knowledge on working with different types of shells.
> A visual summary of the modules covered in this path: credential attacks, enumeration, shell management, and SQL injection.

---

## 🛠️ Included Modules

---

### 1. 🐍 Hydra - Network Logon Cracker

![Hydra Module](https://github.com/user-attachments/assets/c92e68b2-fc94-45a9-aed9-c31e5ca4e29f)


#### 🔍 Description:
Hydra is a **fast and flexible brute-force password-cracking tool**. It supports many protocols (FTP, SSH, Telnet, HTTP, SMB, etc.) and allows automated login attempts using wordlists.

#### 📚 What You'll Learn:
- How Hydra works and when to use it
- Using username/password wordlists
- Brute-forcing against various network services
- Interpreting output and understanding success indicators

#### 💻 Example Usage:
```bash
hydra -L users.txt -P passwords.txt ssh://10.10.10.10
hydra -l admin -P /usr/share/wordlists/rockyou.txt ftp://<target-ip>
```

#### ✅ Real-World Use Cases:
- Testing default and weak credentials on exposed services
- Credential stuffing during web app testing

---

### 2. 🧭 Gobuster - Directory and File Enumeration

![Gobuster Module](https://github.com/user-attachments/assets/c1c17753-bc35-44c1-a338-991b6b0a7dbf)


#### 🔍 Description:
Gobuster is a powerful **brute-force enumeration tool** for web content. It discovers hidden files and directories by requesting known paths using wordlists.

#### 📚 What You'll Learn:
- Wordlist-based directory enumeration
- Finding hidden folders, login panels, backups, `.php~` or `.bak` files
- Performing virtual host brute-forcing

#### 💻 Example Usage:
```bash
gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html,txt
```

#### ✅ Real-World Use Cases:
- Discovering admin panels (`/admin`)
- Locating forgotten or misconfigured files (`/backup.zip`, `/login.php`)

---

### 3. 🐚 Shells Overview - Bind, Reverse, Web Shells

![Shells Module](https://github.com/user-attachments/assets/2e80b66f-314c-4f42-a59b-a1127345db73)


#### 🔍 Description:
Learn the **types of shells** attackers use to gain access to systems after successful exploitation. Understand the differences and when to use each.

#### 📚 What You'll Learn:
- Bind shell vs Reverse shell
- Web shell examples (e.g., PHP shells)
- Netcat usage for manual shells
- How to upgrade a limited shell to fully interactive (`python`, `script`, `SUID bash`, etc.)

#### 💻 Shell Upgrade Example:
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
CTRL+Z
stty raw -echo; fg
```

#### ✅ Real-World Use Cases:
- Maintaining access after gaining initial shell
- Preparing for privilege escalation or lateral movement

---

### 4. 💉 SQLMap - SQL Injection Automation

![SQLMap Module](https://github.com/user-attachments/assets/be65d4ff-7b96-40a3-a243-d6dfac0567ce)


#### 🔍 Description:
SQLMap is a **fully automated SQL injection exploitation tool**. It helps identify injection points and extract data from vulnerable databases.

#### 📚 What You'll Learn:
- Basic and advanced usage of SQLMap
- Using `--dump` to extract database tables
- Authentication bypass via SQLi
- Enumerating databases, users, passwords
- Tampering and evading WAFs

#### 💻 Example Usage:
```bash
sqlmap -u "http://target.com/product.php?id=2" --batch --dbs
sqlmap -r request.txt --dbs
```

#### ✅ Real-World Use Cases:
- Dumping credentials from a backend DB
- Exploiting blind or error-based SQLi
- Using tamper scripts to bypass filters

---

## 🎯 Learning Outcomes

By completing this path, you will be able to:
- Perform **brute-force attacks** against services using Hydra
- Discover hidden directories/files with Gobuster
- Understand and manage different types of shells
- Automate SQL injection exploitation with SQLMap

This path provides essential skills for anyone preparing for:
- CTF competitions
- Bug bounty programs
- Red teaming operations
- Junior penetration testing roles

---

## 👨‍🏫 Who Should Take This Path?

- 🧑‍💻 Beginners in penetration testing
- 🎯 CTF players looking to master core tools
- 🔐 Cybersecurity students and red teamers
- 🐞 Bug bounty hunters exploring automation

---

## 🧰 Tools Summary

| Tool      | Function                        | Protocols/Targets            |
|-----------|----------------------------------|------------------------------|
| Hydra     | Credential brute-force          | SSH, FTP, HTTP, RDP, SMB     |
| Gobuster  | Web directory enumeration        | HTTP(S)                      |
| Shells    | Interactive remote access        | Bash, Netcat, Web shells     |
| SQLMap    | SQL injection automation         | MySQL, PostgreSQL, MSSQL     |

---

## 📚 Resources

- [TryHackMe Path](https://tryhackme.com/path/preview/offensive-security-tooling)
- [Hydra GitHub](https://github.com/vanhauser-thc/thc-hydra)
- [Gobuster GitHub](https://github.com/OJ/gobuster)
- [SQLMap Project](https://sqlmap.org)
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)
