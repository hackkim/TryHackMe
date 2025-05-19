# 🔐 TryHackMe: Network Security - Protocols and Servers 2

This document thoroughly explores attacks targeting common networking protocols and outlines modern mitigation techniques.

---

## ✅ Task 1 - Introduction

We revisit these protocols:

* Telnet
* HTTP
* FTP
* SMTP
* POP3
* IMAP

These protocols are subject to various **security attacks**, including:

1. **Sniffing Attack** – capturing cleartext traffic
2. **Man-in-the-Middle (MITM)** – altering communication without detection
3. **Password Attack** – brute force and dictionary attacks

### 🔒 CIA vs DAD

* **CIA Triad**: Confidentiality, Integrity, Availability
* **DAD Threats**: Disclosure, Alteration, Destruction

These map directly:

| CIA                          | DAD |
| ---------------------------- | --- |
| Confidentiality → Disclosure |     |
| Integrity → Alteration       |     |
| Availability → Destruction   |     |

![CIA vs DAD Triad](https://github.com/user-attachments/assets/74f79b51-2ad8-4d88-b2ad-ceb77584265d)

This room focuses on safeguarding **Confidentiality** and **Integrity**.

---

## 🕵️ Task 2 - Sniffing Attack

A **sniffing attack** captures packets over a network. If data is transmitted unencrypted (cleartext), sensitive information such as usernames and passwords can be retrieved.

**Common tools**:

* `tcpdump`
* `Wireshark`
* `tshark`

**Example using tcpdump**:

```bash
sudo tcpdump port 110 -A
```

**Captured packet:**

* `USER frank`
* `PASS D2xc9CgD`

![POP3 Sniffing Packet Capture](https://github.com/user-attachments/assets/1262e63f-cf56-452b-9d3a-f618db0809ff)

### 🔐 Mitigation

* Use **TLS** for encryption
* Avoid cleartext protocols (replace Telnet with SSH)

---

## 🤔 Task 3 - Man-in-the-Middle (MITM) Attack

In a **MITM attack**, the attacker (E) intercepts communication between a client (A) and server (B), potentially altering the content.

Example: A transfers \$20 to M; E changes it to \$2000.

![Man-in-the-Middle Attack Example](https://github.com/user-attachments/assets/31fe607f-d545-48aa-a953-2f432408c215)

### 🔐 Mitigation

* Use **encryption (TLS)**
* Implement **authentication and integrity checks**
* Employ **PKI** and **trusted certificates**

---

## 🔒 Task 4 - Transport Layer Security (TLS)

TLS protects data at the **presentation layer** (Layer 6), encrypting data from application-layer protocols like HTTP, FTP, SMTP, etc.

![TLS at OSI Layers](https://github.com/user-attachments/assets/86b99a2a-7d7c-48c7-9cc9-d81feb63d34e)

**Default TLS ports**:

| Protocol | Clear Port | TLS Port |
| -------- | ---------- | -------- |
| HTTP     | 80         | 443      |
| FTP      | 21         | 990      |
| SMTP     | 25         | 465      |
| POP3     | 110        | 995      |
| IMAP     | 143        | 993      |

### TLS Handshake (RFC 6101)

1. `ClientHello`
2. `ServerHello` + Certificate
3. `KeyExchange` + Cipher agreement
4. `ChangeCipherSpec` + Encrypted communication

![TLS Handshake Process](https://github.com/user-attachments/assets/22c43f27-101a-4471-9abb-4ce8e4641028)

### Certificate Verification

![SSL Certificate Example](https://github.com/user-attachments/assets/e3e2628d-9393-44f4-8207-4e18e0d4beea)

---

## 🔏 Task 5 - Secure Shell (SSH)

SSH is the **secure alternative to Telnet**, used for encrypted remote access and file transfers.

* **Port:** 22
* Supports **password** or **key-based authentication**
* Enables **SCP** and **SFTP** for secure file transfer

### Example

```bash
ssh mark@MACHINE_IP
scp file.txt mark@MACHINE_IP:/home/mark
```

### MITM in SSH

If the public key fingerprint isn’t verified, MITM is possible.

![SSH MITM Attack Example](https://github.com/user-attachments/assets/7ee7435b-59f8-415f-b5fe-017ae15771ed)

---

## 🔐 Task 6 - Password Attack

Protocols like Telnet, FTP, POP3, and IMAP often require **username/password authentication**. These can be attacked via:

1. **Guessing** – based on known information
2. **Dictionary attack** – using known wordlists
3. **Brute force** – trying all combinations

### Wordlist

* `/usr/share/wordlists/rockyou.txt`

### THC Hydra

```bash
hydra -l USERNAME -P wordlist.txt TARGET SERVICE
```

**Examples**:

```bash
hydra -l frank -P rockyou.txt MACHINE_IP ssh
hydra -l mark -P rockyou.txt ftp://MACHINE_IP
```

**Useful Flags**:

* `-V` verbose output
* `-t` threads
* `-d` debug

### 🔐 Mitigation

* Strong password policies
* Account lockouts / throttling
* CAPTCHA / 2FA
* Public key authentication (SSH)

---

## 📊 Task 7 - Summary

### 🤖 Attacks Covered

1. Sniffing
2. MITM
3. Password Attacks

### 📈 Protocol Comparison

| Protocol | TCP Port | Application(s)                  | Data Security |
|----------|----------|----------------------------------|----------------|
| FTP      | 21       | File Transfer                   | ❌ Cleartext   |
| FTPS     | 990      | File Transfer                   | ✅ Encrypted   |
| HTTP     | 80       | Worldwide Web                   | ❌ Cleartext   |
| HTTPS    | 443      | Worldwide Web                   | ✅ Encrypted   |
| IMAP     | 143      | Email (MDA)                     | ❌ Cleartext   |
| IMAPS    | 993      | Email (MDA)                     | ✅ Encrypted   |
| POP3     | 110      | Email (MDA)                     | ❌ Cleartext   |
| POP3S    | 995      | Email (MDA)                     | ✅ Encrypted   |
| SFTP     | 22       | File Transfer (via SSH)         | ✅ Encrypted   |
| SSH      | 22       | Remote Access, File Transfer    | ✅ Encrypted   |
| SMTP     | 25       | Email (MTA)                     | ❌ Cleartext   |
| SMTPS    | 465      | Email (MTA)                     | ✅ Encrypted   |
| Telnet   | 23       | Remote Access                   | ❌ Cleartext   |

### 🔧 Hydra Options Summary

| Option | Description |
| ------ | ----------- |
| -l     | username    |
| -P     | wordlist    |
| -s     | custom port |
| -V     | verbose     |
| -t     | threads     |
| -d     | debug mode  |

---

Explore more via:

* Vulnerability Research
* Metasploit
* Burp Suite

Stay secure! ✨
