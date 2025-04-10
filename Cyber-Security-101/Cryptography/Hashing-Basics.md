# 🔐 TryHackMe - Hashing Basics

Welcome to the third room in TryHackMe’s foundational cryptography path. In this room, we explore **hashing** — what it is, how it's used, and why it's crucial for security in authentication systems and data integrity verification.

---

## 🧠 Task 1: Introduction

![Hashing Intro Scene](https://github.com/user-attachments/assets/a20d9ddc-9870-4c19-acba-133f995c64f7)

Imagine downloading a 6GB file. How do you verify that your downloaded file is **identical to the original** and hasn’t been tampered with?

🧪 **Answer**: Use a hash function to compare the **hash values** of both files.

### ✅ What is a Hash?
- A **hash value** is a fixed-size string produced by a **hash function**.
- A **hash function** takes input of any length and returns a unique, fixed-length digest.

📌 Terms:
- **Hash** (noun): the output of a hash function
- **To hash** (verb): the act of computing a hash value

### 📘 Prerequisite Rooms
- Cryptography Basics ✅
- Public Key Cryptography Basics ✅
- Hashing Basics 🟢 (this room)

### 🎯 Learning Objectives
- Understand hashing & collisions
- Learn how hashes are stored and cracked
- Use hashing for password and integrity verification

---

## 🔁 Task 2: Hash Functions

### 🔍 Definition
A **hash function**:
- Accepts any input size
- Outputs fixed-length string (digest)
- **One-way only**: You can’t reverse a hash
- A small input change → drastically different hash (avalanche effect)

### 🧪 Example: Comparing `T` vs `U`
Both differ by **one bit** (ASCII: 01010100 vs 01010101)

#### Output comparison:
```bash
md5sum file1.txt file2.txt
sha1sum file1.txt file2.txt
sha256sum file1.txt file2.txt
```

### 🔐 Real Use Cases
- Password verification
- File download validation
- Digital signatures (via hash of document)

---

### ⚠️ Hash Collisions

- When **two different inputs produce the same output**
- Collisions are **inevitable** due to limited output space (Pigeonhole Principle)
- Good hash functions make collisions **computationally infeasible**

| Algorithm | Status     |
|-----------|------------|
| MD5       | Broken     |
| SHA-1     | Broken     |
| SHA-256   | Secure ✅  |

📚 See:
- [MD5 Collision Demo](https://www.mscs.dal.ca/~selinger/md5collision/)
- [SHA1 Collision (SHAttered)](https://shattered.io/)

---

## 🚫 Task 3: Insecure Password Storage

### 🔓 Bad Practices:
1. **Plaintext Storage**
   - e.g. RockYou database breach → over 14M passwords leaked
   - Password list reused in pentesting (`rockyou.txt`)
2. **Weak Encryption**
   - Adobe used reversible encryption, and stored hints in plaintext
3. **Insecure Hashing**
   - LinkedIn breach: SHA-1, no salting → easy to crack

### 📂 Example: `rockyou.txt`
```bash
wc -l /usr/share/wordlists/rockyou.txt
head /usr/share/wordlists/rockyou.txt
```

---

## 🔐 Task 4: Using Hashing for Secure Password Storage

### ✅ Secure Approach:
1. Add a **salt** (random string)
2. Concatenate password + salt
3. Use strong hash: **Bcrypt**, **Scrypt**, **Argon2**
4. Store the resulting hash + the salt

| Step | Value                            |
|------|----------------------------------|
| PW   | AL4RMc10k                        |
| Salt | Y4UV*^(=go_!                     |
| Hash Input | AL4RMc10kY4UV*^(=go_!      |
| Final Hash | [SecureHash]               |

![CrackStation Lookup Example](https://github.com/user-attachments/assets/a3663c9b-9cf3-4736-afe3-4d97dbdad972)

### ⚠️ Rainbow Tables
- Precomputed hash→password maps
- Fast lookup if no salt is used
- Sites like hashes.com use massive tables

### ✅ Salting Defeats Rainbow Tables

---

## 🔍 Task 5: Recognizing Password Hashes

### 🔐 Linux Style Hashes
Format: `$id$options$salt$hash`

| Prefix | Algorithm     |
|--------|---------------|
| `$y$`  | yescrypt      |
| `$2a$` | bcrypt        |
| `$6$`  | SHA512-crypt  |
| `$1$`  | MD5-crypt     |

```bash
grep username /etc/shadow
man 5 shadow
```

### 🪟 Windows (NTLM)
- Stored in **SAM**
- Extract with tools like `mimikatz`, `secretsdump`
- Algorithm: NTLM = MD4 variant

🔍 More examples: [Hashcat Example Hashes](https://hashcat.net/wiki/doku.php?id=example_hashes)

---

## 💥 Task 6: Password Cracking

### 🛠️ Tools
- **Hashcat** (GPU-based)
- **John the Ripper** (CPU-based)

### 🧪 Crack with Wordlist
```bash
hashcat -m 0 -a 0 hashes.txt rockyou.txt
```

| Flag | Description              |
|------|--------------------------|
| `-m` | Hash type ID (e.g., 1000 = NTLM) |
| `-a` | Attack mode (0 = straight)      |

💡 VMs slow down GPU cracking → Run on host!

---

## 🧾 Task 7: Hashing for Integrity

### ✅ File Check
If downloaded file hash = official hash → file is valid

```bash
sha256sum myfile.iso
# Compare to official site value
```

![HMAC Construction Diagram](https://github.com/user-attachments/assets/e5af0da2-42e8-4059-9f54-677e6ff832c1)

### 🔐 HMAC (Hash-based Message Authentication Code)

Formula:
```
HMAC(K, M) = H((K ⊕ opad) || H((K ⊕ ipad) || M))
```

Used to:
- Prove authenticity (K = secret key)
- Prove integrity (H = hash function)

Used in:
- APIs
- Digital signature schemes
- JWT verification

---

## ✅ Task 8: Conclusion

### 🔁 Comparison Table

| Type       | Direction | Purpose                      | Reversible |
|------------|-----------|------------------------------|------------|
| Hashing    | One-way   | Integrity, Auth              | ❌         |
| Encoding   | Two-way   | Data formatting              | ✅         |
| Encryption | Two-way   | Confidentiality              | ✅         |

#### 📦 Base64 Example
```bash
echo "TryHackMe" | base64
echo "VHJ5SGFja01lCg==" | base64 -d
```

### 🔐 Key Takeaways
- Always hash passwords securely using salts
- Don’t trust MD5/SHA1
- Use HMAC for integrity + authentication
- Learn to **recognize** and **crack** hashes responsibly

➡️ **Next Room**: John the Ripper
