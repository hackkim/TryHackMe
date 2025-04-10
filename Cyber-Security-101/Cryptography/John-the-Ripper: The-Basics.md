# 🔐 TryHackMe - John the Ripper: The Basics

Welcome to **John the Ripper (JtR)** — one of the most powerful and flexible password hash-cracking tools. This room provides comprehensive guidance on using JtR to crack common hashes, authentication files, archive passwords, and SSH private key passphrases.

---

## 🧠 Task 1: Introduction

![John the Ripper Intro Scene](https://github.com/user-attachments/assets/7023bdab-4a0d-48c4-85cc-3772dc3f40c5)

John the Ripper:
- Built for **cracking password hashes**
- Supports **dictionary**, **brute-force**, and **custom rules**
- Can crack:
  - NTLM (Windows)
  - `/etc/shadow` (Linux)
  - ZIP & RAR files
  - Encrypted SSH private keys

### 🔐 Prerequisites:
- Cryptography Basics
- Public Key Cryptography Basics
- Hashing Basics

---

## 🔑 Task 2: Basic Terms

### What is a Hash?
- One-way transformation: input → fixed-length output
- Common formats: MD5, SHA1, NTLM, SHA-512
- Not reversible but vulnerable to **brute-force** and **dictionary** attacks

### Mathematical Context
- Hashing = easy (`P`)
- Reversing = hard (`NP`)
- Cracking = guessing via hashing dictionary words

---

## ⚙️ Task 3: Setting Up Jumbo John

### 💻 Use Jumbo John (extended version):
- Includes tools: `zip2john`, `rar2john`, `ssh2john`, `unshadow`

### ✅ Pre-installed on:
- TryHackMe AttackBox
- Kali Linux

### 🛠️ Manual install:
```bash
sudo apt install john
```

### 📦 Wordlists:
```bash
/usr/share/wordlists/rockyou.txt
```

For custom install & full features: https://github.com/openwall/john

---

## 🔐 Task 4: Cracking Basic Hashes

### John syntax:
```bash
john [options] [hashfile]
```

### Dictionary attack:
```bash
john --wordlist=rockyou.txt hashes.txt
```

### Hash identification:
- Use `hash-identifier`
- Or visit: https://hashes.com/en/tools/hash_identifier

### Format-specific cracking:
```bash
john --format=raw-md5 --wordlist=rockyou.txt hashes.txt
```

Check formats:
```bash
john --list=formats | grep sha
```

---

## 🪟 Task 5: Cracking NTLM Hashes

### What is NTLM?
- Used in Windows systems (stored in SAM/NTDS.dit)
- Retrieved via tools like **mimikatz**

### Crack with John:
```bash
john --format=nt --wordlist=rockyou.txt ntlm.txt
```

---

## 🐧 Task 6: Cracking /etc/shadow Hashes

### Step 1: Merge passwd & shadow
```bash
unshadow passwd shadow > combined.txt
```

### Step 2: Crack
```bash
john --format=sha512crypt --wordlist=rockyou.txt combined.txt
```

Use full lines or only user entries:
```bash
root:x:0:0::/root:/bin/bash
root:$6$saltsalt$hashhash...
```

---

## 🧠 Task 7: Single Crack Mode

JtR uses username + GECOS field to generate guesses.

### Example: Username "Markus"
Guesses: Markus1, Markus$, MArkus, etc.

### Command:
```bash
john --single --format=raw-sha256 hashes.txt
```

### File Format:
```
username:hash
```

---

## ⚙️ Task 8: Custom Rules

Defined in:
```bash
/etc/john/john.conf
```

### Example Rule:
```ini
[List.Rules:THMRules]
cAz"[0-9][!@#$]"
```

- `c` = Capitalize
- `Az` = Append number + symbol

### Use Rule:
```bash
john --wordlist=rockyou.txt --rules=THMRules hashes.txt
```

Explore examples: around line 678 in `john.conf`

---

## 🗜️ Task 9: Cracking ZIP Files

### Step 1: Convert with zip2john
```bash
zip2john secret.zip > zip_hash.txt
```

### Step 2: Crack:
```bash
john --wordlist=rockyou.txt zip_hash.txt
```

---

## 📦 Task 10: Cracking RAR Files

### Step 1: Convert:
```bash
rar2john secure.rar > rar_hash.txt
```

### Step 2: Crack:
```bash
john --wordlist=rockyou.txt rar_hash.txt
```

---

## 🔐 Task 11: Cracking SSH Private Key Passphrases

### Step 1: Extract hash:
```bash
/opt/john/ssh2john.py id_rsa > rsa_hash.txt
```

or:
```bash
python3 /usr/share/john/ssh2john.py id_rsa > rsa_hash.txt
```

### Step 2: Crack:
```bash
john --wordlist=rockyou.txt rsa_hash.txt
```

---

## 📚 Task 12: Further Reading

You now know how to:
- Identify and crack hashes
- Use `zip2john`, `rar2john`, `ssh2john`, and `unshadow`
- Apply single mode and custom rules

### 📌 Explore More:
- [Openwall John Wiki](https://openwall.info/wiki/john)
- TryHackMe’s advanced cryptography & OSINT rooms

