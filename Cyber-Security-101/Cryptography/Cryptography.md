# 🔐 TryHackMe - Cryptography Path

> Explore various symmetric and asymmetric encryption algorithms. Discover the usage of hashing algorithms in everyday systems.

![Cryptography Intro](https://github.com/user-attachments/assets/74fb9d3f-07e6-400c-95dc-2d378b48f8a9)

---

## ✅ 1. Cryptography Basics

![Cryptography Basics](https://github.com/user-attachments/assets/0931d69a-573d-48e0-9fa3-40fa52bc2c3e)

### 📌 What You Learn
- What is cryptography?
- Difference between symmetric and asymmetric encryption
- Basic terminologies: plaintext, ciphertext, encryption key, decryption key
- Examples of symmetric algorithms: AES, DES

### 🧠 Key Concepts
- **Symmetric Encryption:** Uses the same key for encryption and decryption.
- **Block vs Stream Ciphers:** Block ciphers encrypt fixed-size blocks, stream ciphers encrypt one bit/byte at a time.

---

## ✅ 2. Public Key Cryptography Basics

![Public Key Cryptography Basics](https://github.com/user-attachments/assets/c52feacd-3ca7-48ec-9627-f953586c7ca7)

### 📌 What You Learn
- Introduction to asymmetric encryption
- Public key vs Private key
- How RSA encryption works
- Real-world usage: **SSH**, **Digital Signatures**

### 🔐 Key Concepts
- **Asymmetric Encryption:** Uses a pair of keys — public and private.
- **RSA:** A widely-used public key algorithm.
- **SSH Key Authentication:** Uses asymmetric encryption to securely connect to servers.

---

## ✅ 3. Hashing Basics

![Hashing Basics](https://github.com/user-attachments/assets/a74ce005-6fb3-4df7-9f92-37e5e34642d9)

### 📌 What You Learn
- What is a hash function?
- Characteristics of good hash functions (deterministic, fast, irreversible, collision-resistant)
- Popular hashing algorithms: MD5, SHA-1, SHA-256

### 🔍 Use Cases
- **Password verification**
- **File integrity checking**
- **Digital signatures**

### 🧪 Examples
```bash
# Hash a file with sha256sum
sha256sum example.txt
```

---

## ✅ 4. John the Ripper: The Basics

![John the Ripper](https://github.com/user-attachments/assets/f769ee89-c694-4641-bbaf-3b78cba53c28)

### 📌 What You Learn
- Introduction to John the Ripper (JtR)
- How to use it for cracking password hashes
- Wordlist attacks using `rockyou.txt`
- Format conversion (e.g., `/etc/shadow` into hash format)

### 🧪 Common Commands
```bash
# Basic usage with wordlist
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

# Show cracked passwords
john --show hashes.txt
```

### 🧠 Tip
- Always identify the hash format using `--format` if JtR doesn't auto-detect.
- Use `unshadow` to combine passwd and shadow files.

---

## 📊 Summary

| Topic                         | Key Tools / Concepts              | Practical Use                          |
|------------------------------|-----------------------------------|----------------------------------------|
| Cryptography Basics          | AES, DES, XOR                     | Data protection                        |
| Public Key Cryptography      | RSA, SSH, Key pairs               | Secure communication                   |
| Hashing Basics               | SHA-256, MD5                      | Passwords, integrity check             |
| John the Ripper              | JtR, rockyou.txt, unshadow        | Password cracking for red team tasks   |

---

✅ **Completed:** All tasks in the Cryptography module  
📚 **Next Steps:** Explore more tools like `GPG`, `Hydra`, or dive into `Password Cracking` room
