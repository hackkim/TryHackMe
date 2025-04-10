# 🔐 TryHackMe - Public Key Cryptography Basics

This room is the second part of the Cryptography series on TryHackMe. It focuses on **asymmetric encryption**, how it works, and how it's used in real-world systems such as **RSA**, **Diffie-Hellman**, **SSH**, **TLS/SSL**, and **PGP/GPG**.

---

## 🧠 Task 1: Introduction

![Public Key Cryptography Intro](https://github.com/user-attachments/assets/18d648c8-ad1c-49ca-b34e-07cb2c8852dd)

Imagine a real-world meeting with a business partner. You rely on:
- Seeing and hearing the other person (**authentication**)
- Confirming the origin and accuracy of what they say (**authenticity & integrity**)
- Whispering so only they hear (**confidentiality**)

In cyberspace, cryptography provides these guarantees:
- 🔐 **Authentication** – verifying identity
- 🔒 **Confidentiality** – ensuring privacy
- 📦 **Integrity** – confirming data is unaltered
- 🧾 **Authenticity** – confirming the sender

### 🤝 Symmetric vs Asymmetric Cryptography
- **Symmetric Encryption**: Same key for encryption & decryption.
- **Asymmetric Encryption**: Public key to encrypt, private key to decrypt. Enables secure authentication, integrity, and trust without shared secrets.

### 📘 Prerequisites
Ensure completion of:
1. ✅ Cryptography Basics
2. 🟦 **Public Key Cryptography Basics (this room)**
3. 🕹️ Hashing Basics

---

## 🔁 Task 2: Common Use of Asymmetric Encryption

### 🎯 Goal: Securely agree on a symmetric encryption key over an insecure network.

Asymmetric encryption is **computationally expensive**, so it's mainly used to **exchange symmetric keys** securely.

#![Encrypted Lockbox Analogy](https://github.com/user-attachments/assets/69e087d5-5de9-4522-bc3e-0146f7b220ab)

### 🔐 Real-World Analogy

| Concept         | Cryptographic Term              |
|------------------|---------------------------------|
| Secret Code      | Symmetric key + cipher          |
| Lock             | Public key                      |
| Lock's Key       | Private key                     |

Once the symmetric key is shared using asymmetric encryption, communication continues using faster **symmetric encryption**.

### 🌐 Real World Application
- Web browsers use asymmetric encryption (e.g., RSA) to establish a secure session (TLS).
- Session continues via symmetric encryption (e.g., AES).

---

## 🔑 Task 3: RSA (Rivest-Shamir-Adleman)

### 📌 What is RSA?
A public-key encryption algorithm based on the **difficulty of factoring large numbers**.

![RSA Encryption and Decryption](https://github.com/user-attachments/assets/3a241be3-f936-480a-9db6-a6ede59f108f)

### 🔐 Key Concepts:
- Easy to multiply large primes
- Very hard to factor the result
- Secure because of this imbalance

#### 🧮 Example:
Let:
- `p = 157`, `q = 199`
- `n = p * q = 31243`
- φ(n) = (p - 1)(q - 1) = 30888

Choose:
- `e = 163` (public exponent)
- `d = 379` such that `e * d ≡ 1 (mod φ(n))`

Keys:
- Public: (n, e)
- Private: (n, d)

Encrypt: `c = m^e mod n`  
Decrypt: `m = c^d mod n`

#### 🧠 CTF Variable Guide:
- `p, q` – prime factors
- `n` – modulus
- `e` – public exponent
- `d` – private exponent
- `m` – original message
- `c` – ciphertext

#### 🧰 Useful Tools:
- `RsaCtfTool`
- `rsatool`

---

## 🔁 Task 4: Diffie-Hellman Key Exchange

### 🎯 Purpose:
Establish a shared symmetric key over an insecure channel — without sending the key directly.

![Diffie-Hellman Key Exchange](https://github.com/user-attachments/assets/b3414f14-4172-488f-9f32-8b922998edc6)

### 🔐 Steps (simplified):
1. Public values: `p = 29`, `g = 3`
2. Alice chooses secret `a = 13`, Bob chooses `b = 15`
3. Public keys:
   - Alice: `A = g^a mod p = 19`
   - Bob: `B = g^b mod p = 26`
4. Shared key:
   - Alice: `B^a mod p = 10`
   - Bob: `A^b mod p = 10`

💡 Shared secret `gab mod p` is the same on both ends.

> Often used alongside RSA: RSA handles authentication, Diffie-Hellman handles secure key agreement.

---

## 🖥️ Task 5: SSH Authentication

### ✅ Server Authentication
- Server sends its **public key fingerprint**
- Client checks if it's **known/trusted**
- Prevents **Man-In-The-Middle** (MITM) attacks

### ✅ Client Authentication
- Client uses public/private key pair
- Server authenticates the user via **public key match**

#### 🔐 SSH Key Generation
```bash
ssh-keygen -t ed25519
```

#### 📁 Key Files:
- `id_ed25519` → private key (keep secure!)
- `id_ed25519.pub` → public key (can be shared)

#### 📋 Best Practices:
- Use strong passphrase
- Permissions: `chmod 600 id_ed25519`
- Store keys in `~/.ssh/`

---

## ✍️ Task 6: Digital Signatures & Certificates

### 🔏 Digital Signatures:
- Private key is used to **sign a document**
- Public key is used to **verify the signature**

![Digital Signature Process](https://github.com/user-attachments/assets/bcf79bfe-dd2c-42b5-bdc8-433071630958)

🧾 Proves:
- Document came from you
- Document hasn’t been altered

### 📜 Certificates:
Used in HTTPS (e.g., tryhackme.com).
- Contains public key + domain info
- Signed by trusted Certificate Authorities (CAs)

📦 Chain of Trust:
1. Site Certificate
2. Intermediate CA
3. Root CA (trusted by browsers)

---

## 📧 Task 7: PGP and GPG

### 🛡️ What is GPG?
- **PGP**: Pretty Good Privacy
- **GPG**: GNU Privacy Guard, open-source implementation

Used to:
- Encrypt files/emails
- Sign digital content

#### 🔐 Generate a Key
```bash
gpg --full-gen-key
```

Choose:
- Algorithm (ECC recommended)
- Expiration date
- Name & Email

#### 🔁 Common Commands
```bash
gpg --import mykey.key
gpg --decrypt message.gpg
```

💡 Use `gpg2john` + `JohnTheRipper` for key cracking in CTFs.

---

## ✅ Task 8: Conclusion

### Summary of Terms

| Term              | Description                                                   |
|-------------------|---------------------------------------------------------------|
| Cryptography      | Securing communication using algorithms and keys              |
| Cryptanalysis     | Breaking/bypassing cryptographic protection                    |
| Brute-force       | Trying all possible combinations                              |
| Dictionary attack | Using common passwords from a wordlist                        |

---

### 🧠 In This Room You Learned:
- 📌 Why asymmetric encryption matters
- 🔐 How RSA secures communication
- 🔁 How Diffie-Hellman exchanges keys
- 🖥️ How SSH uses key-based login
- ✍️ What digital signatures and certificates are
- 📧 How GPG/PGP is used for signing and encryption

➡️ Next: **Hashing Basics**

