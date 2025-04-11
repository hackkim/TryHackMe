# 🔍 TryHackMe - Gobuster: The Basics (Comprehensive Guide)

This markdown is a complete walkthrough and summary of the **Gobuster** TryHackMe room. Gobuster is a powerful and fast brute-force tool used in reconnaissance to discover hidden directories, files, subdomains, and virtual hosts.

---

## 🧠 Task 1 - Introduction


![Gobuster Intro Image](https://github.com/user-attachments/assets/506cc3cb-c2c2-47c4-8785-a024d510f999)


### 🔧 What Is Gobuster?

Gobuster is an open-source tool written in **Go**. It is used to brute-force:
- Web directories and files
- DNS subdomains
- Virtual hosts (vhosts)
- Amazon S3 buckets
- Google Cloud buckets

### 🎯 Learning Goals:
- Understand how brute-force and enumeration work
- Learn the different Gobuster modes (`dir`, `dns`, `vhost`)
- Practice using wordlists for efficient reconnaissance

---

## 🖥️ Task 2 - Environment Setup

The room uses an Ubuntu 20.04 server with:
- Web server hosting multiple **subdomains** and **virtual hosts**
- Installed CMS platforms: **WordPress** and **Joomla**

### 🛠️ DNS Configuration (on AttackBox):
```bash
sudo nano /etc/resolv-dnsmasq
# Add:
nameserver MACHINE_IP
nameserver 169.254.169.253

# Restart DNS service:
sudo /etc/init.d/dnsmasq restart
```

---

## 📘 Task 3 - Gobuster Overview

### 💡 What Is Enumeration?

Enumeration is listing available but possibly hidden resources (e.g., `/admin`, `/config`).

### 🔐 What Is Brute Force?

Trying many values (from a wordlist) until one works, like guessing keys to a lock.

### 📜 Gobuster Help Menu
```bash
gobuster --help
```

### 🔑 Core Commands:
- `dir` — Enumerate directories and files
- `dns` — Enumerate subdomains
- `vhost` — Enumerate virtual hosts
- `s3`, `gcs` — Enumerate cloud buckets
- `fuzz` — Replace the keyword `FUZZ` in URLs or headers

### 🧾 Common Flags:
| Short | Long           | Description |
|-------|----------------|-------------|
| `-u`  | `--url`        | Target URL |
| `-w`  | `--wordlist`   | Wordlist path |
| `-t`  | `--threads`    | Concurrent threads |
| `-r`  | `--followredirect` | Follow redirects |
| `-o`  | `--output`     | Save output to a file |
|       | `--delay`      | Delay between requests |
|       | `--debug`      | Enable debug mode |

---

## 📂 Task 4 - Use Case: Directory and File Enumeration

### 🔎 Mode: `dir`

Brute-force directories or files in a website.

#### 🧪 Example:
```bash
gobuster dir -u http://example.thm -w /usr/share/wordlists/dirb/small.txt -t 50
```

#### 🔧 Extensions:
```bash
gobuster dir -u http://example.thm -w /usr/share/wordlists/dirb/common.txt -x .php,.txt
```

#### 🔐 Authenticated Scans:
```bash
gobuster dir -u http://example.thm -w list.txt -U admin -P pass123
```

---

## 🌐 Task 5 - Use Case: Subdomain Enumeration

### 🔎 Mode: `dns`

Brute-force DNS subdomains (e.g., `admin.example.thm`).

#### 🧪 Example:
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

#### 🔧 Useful Flags:
| Flag | Description |
|------|-------------|
| `-d` | Domain name |
| `-r` | Custom resolver |
| `-i` | Show resolved IPs |
| `-c` | Show CNAME records |

---

## 🏢 Task 6 - Use Case: Vhost Enumeration

### 🔎 Mode: `vhost`

Enumerate virtual hosts hosted on the same IP.

#### 🧪 Example:
```bash
gobuster vhost -u http://10.10.10.10 --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```

#### 🧩 Explanation:
- `--append-domain`: Adds `.example.thm` to each word
- `--exclude-length`: Filters out typical false positives
- `-u`: Target base URL
- `--domain`: Explicitly define domain
- `-w`: Wordlist used for vhost names

---

## ✅ Task 7 - Conclusion

### 📌 Recap of Modes:
| Mode | Purpose |
|------|---------|
| `dir` | Find directories/files |
| `dns` | Discover subdomains |
| `vhost` | Identify virtual hosts |

### 🧠 Key Takeaways:
- Use correct flags for each mode
- Know how to read status codes (`200 OK`, `403 Forbidden`, `301 Redirect`)
- Use filtered output or `--exclude-length` for cleaner results
- Always validate discovered endpoints manually

---

## 📚 Resources

- [TryHackMe Gobuster Room](https://tryhackme.com/room/gobuster)
- [Gobuster GitHub](https://github.com/OJ/gobuster)
- [SecLists Wordlists](https://github.com/danielmiessler/SecLists)
- [Gobuster Kali Tool Docs](https://tools.kali.org/information-gathering/gobuster)
