# 🔐 TryHackMe - Cryptography Basics

This room introduces the fundamentals of cryptography, covering key terms, the importance of encryption, historical and modern ciphers, types of encryption, and basic mathematical concepts used in cryptographic algorithms.

---

## 🧠 Task 1: Introduction

![Introduction Scene](https://github.com/user-attachments/assets/89647074-c7f2-42a9-bb5d-67dacaed4e67)

Have you ever wondered how websites or apps prevent third parties from reading your messages? Cryptography allows us to establish **confidential**, **integral**, and **authentic** communication over untrusted networks.

This room is the **first of three** introductory rooms about cryptography:

1. Cryptography Basics (this room)
2. Public Key Cryptography Basics
3. Hashing Basics

> 📌 **Learning Objectives**
- Understand cryptography key terms
- Learn the importance of cryptography
- Explore the Caesar Cipher
- Understand standard symmetric ciphers
- Recognize common asymmetric ciphers
- Learn basic cryptographic math (XOR & modulo)

---

## 🛡️ Task 2: Importance of Cryptography

Cryptography ensures **secure communication** in the presence of adversaries by protecting:

- 🔒 **Confidentiality** — preventing unauthorized access
- 📦 **Integrity** — ensuring data hasn’t been altered
- 🧾 **Authenticity** — verifying the identity of the source

> 🔐 **Real-life Applications**
- Encrypted login credentials (e.g., HTTPS, SSH)
- Secure tunnels (e.g., SSH sessions)
- Online banking and SSL certificates
- File integrity via hash checking

> 🧾 **Regulatory Compliance**
- **PCI DSS**: credit card data (encryption at rest and in motion)
- **HIPAA**, **HITECH** (USA): health data protection
- **GDPR** (EU), **DPA** (UK): general data protection

---

## 🔤 Task 3: Plaintext to Ciphertext

> 🔁 **Encryption Process Overview**

1. **Plaintext** + **Key** + **Cipher** → **Ciphertext**
2. **Ciphertext** + **Key** + **Cipher** → **Plaintext**

![Encryption Process](https://github.com/user-attachments/assets/a7d5f2d4-cb93-469a-8ec2-15e316f7acf2)

![Decryption Process](https://github.com/user-attachments/assets/d0e9c9bd-5e3f-4d17-a2c7-69706667a08b)

### 🧩 Key Terms

| Term         | Description |
|--------------|-------------|
| **Plaintext** | Readable original data (e.g., message, file) |
| **Ciphertext** | Encrypted unreadable version of the plaintext |
| **Cipher** | The algorithm used to perform encryption/decryption |
| **Key** | The secret used by the cipher to transform data |
| **Encryption** | Converts plaintext into ciphertext |
| **Decryption** | Converts ciphertext back into plaintext |

> 🔐 The cipher is usually public, but the **key must remain secret**.

---

## 📜 Task 4: Historical Ciphers

### 🏛️ **Caesar Cipher**

- Simple substitution cipher
- Shifts each letter in the alphabet by a fixed number
- Example:
  - **Plaintext:** TRYHACKME
  - **Key:** 3 (right shift)
  - **Ciphertext:** WUBKDFNPH

> 🔓 **Caesar Cipher is easily breakable** since there are only 25 possible keys.

![Caesar Cipher Encryption](https://github.com/user-attachments/assets/d10af401-55a0-4000-bec2-6febc0bd79f0)

![Caesar Cipher Decryption](https://github.com/user-attachments/assets/270c4a68-a227-4b9a-ba0e-56e668228db5)

![Caesar Cipher Brute Force](https://github.com/user-attachments/assets/fd2ffd69-467a-4229-b5a9-f211cc4c6e97)

### 🕵️‍♂️ Other Historical Ciphers
- **Vigenère Cipher** (16th century)
- **Enigma Machine** (WWII)
- **One-Time Pad** (Cold War)

These are historically significant but insecure by modern standards.

---

## 🔑 Task 5: Types of Encryption

### 🔁 Symmetric Encryption

- Same key used for encryption & decryption
- Key distribution must be secure

![Symmetric Encryption](https://github.com/user-attachments/assets/ccfdb175-c485-4871-8764-994542b66aff)

![Asymmetric Encryption](https://github.com/user-attachments/assets/fe2b7f1d-80fc-4149-830e-97dc08f5f0c9)

#### 🔐 Examples:
| Algorithm | Key Size | Notes |
|-----------|----------|-------|
| DES       | 56-bit   | Broken in 1999 |
| 3DES      | 168-bit  | Deprecated, still used in legacy |
| AES       | 128/192/256-bit | Modern standard |

> 📦 **Problem:** Secure key exchange is difficult when multiple recipients are involved.

---

### 🧩 Asymmetric Encryption

- Uses **two keys**: Public (encrypt), Private (decrypt)
- Known as **public key cryptography**

![Symmetric Encryption](https://github.com/user-attachments/assets/5acfd6c3-c2b6-44a7-bcf2-b076065ccfeb)

![Asymmetric Encryption](https://github.com/user-attachments/assets/3a12f519-cd4c-4e92-bb17-10cae05729e5)

#### 🔐 Examples:
| Algorithm | Key Sizes | Notes |
|-----------|-----------|-------|
| RSA       | 2048/3072/4096 bits | Common standard |
| Diffie-Hellman | ≥2048 bits | Key exchange protocol |
| ECC       | 256 bits (equivalent to RSA 3072) | Efficient with smaller keys |

> 🧠 Based on one-way mathematical problems (hard to reverse)

---

## ➗ Task 6: Basic Mathematics

### ⚙️ XOR (Exclusive OR)

- Bitwise operation: returns `1` if inputs are different, `0` if same

| A | B | A ⊕ B |
|---|---|--------|
| 0 | 0 |   0    |
| 0 | 1 |   1    |
| 1 | 0 |   1    |
| 1 | 1 |   0    |

> 🔐 **Use in encryption**:  
C = P ⊕ K  
P = C ⊕ K

### ➗ Modulo Operation (%)

- Calculates the **remainder** of division

#### 📊 Examples:
- 25 % 5 = 0
- 23 % 6 = 5
- 23 % 7 = 2

> 🔁 Used in many cryptographic algorithms for wrapping values in a defined range (0 to n-1)

---

## 🧾 Task 7: Summary

We explored:

- 🔐 The role of cryptography in secure communication
- 🔄 The difference between symmetric and asymmetric encryption
- 📜 Historical ciphers like Caesar and Enigma
- ⚙️ XOR and modulo operations as mathematical foundations

Next up:  
📘 **Public Key Cryptography Basics** — learn how public key systems like RSA work and power secure applications like SSH.

