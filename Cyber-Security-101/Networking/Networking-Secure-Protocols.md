# 🔐 TryHackMe - Networking Secure Protocols

> This markdown summarizes my learning from the **Networking Secure Protocols** room on TryHackMe.  
> It is the final room in a four-part series focused on securing common network protocols.

---

## 🧠 Task 1 - Introduction

![Networking Secure Protocols Overview](https://github.com/user-attachments/assets/a78dbad7-2c53-4bbd-b83f-ede8d4d8c4db)

While previous rooms explored how web and email protocols work, this room focuses on **securing** those protocols.

### ⚠️ Key Concepts
- **Confidentiality**: Protect data from being read (e.g., passwords, credit cards)
- **Integrity**: Ensure data isn’t tampered with (e.g., changing payment amount)
- **Authenticity**: Ensure you are talking to the real server

### 🧾 Learning Objectives
- TLS and how it secures HTTP, SMTP, POP3, IMAP
- SSH replacing Telnet
- VPNs for secure network communication

---

## 🔐 Task 2 - TLS

![TLS Certificate Authorities](https://github.com/user-attachments/assets/c7659b56-b4ba-489e-8f83-77b30c8c5a2e)

**TLS (Transport Layer Security)** provides confidentiality and integrity over the network.

### 🔑 TLS History Highlights
| Year | Milestone |
|------|-----------|
| 1995 | SSL 2.0 (by Netscape) |
| 1999 | TLS 1.0 released (upgrade to SSL 3.0) |
| 2018 | TLS 1.3 introduces major security improvements |

### 📦 TLS Use Cases
- HTTP → HTTPS
- DNS → DoT (DNS over TLS)
- MQTT → MQTTS
- SIP → SIPS

TLS works at the **Transport Layer (Layer 4)** and encrypts data above it, e.g., HTTP, SMTP, etc.

---

## 🌐 Task 3 - HTTPS

![HTTP Wireshark Stream](https://github.com/user-attachments/assets/6202a092-f287-4ed2-bf69-157f928a5f20)
![HTTP TCP Handshake + GET Flow](https://github.com/user-attachments/assets/f3152a18-1810-4b01-a05a-e1348b6e8b29)
![TLS Handshake and HTTPS Start](https://github.com/user-attachments/assets/e584724d-0f8b-4afd-9f0a-0d7e9dff185b)
![Encrypted HTTPS Stream](https://github.com/user-attachments/assets/53e7bf5b-5446-4ba3-9010-952996d56370)
![Decrypted TLS HTTP Stream](https://github.com/user-attachments/assets/a1af722d-2865-4a1b-8bd9-8634a43ff10d)
![HTTPS HTTP2 GET Login](https://github.com/user-attachments/assets/975f140d-8fa6-4cbf-b9cb-dff9ed79ddb3)

### 🔓 HTTP Flow
1. TCP 3-way handshake
2. Send HTTP request (e.g., `GET /`)
3. Receive HTTP response (HTML, headers, etc.)

### 🔒 HTTPS Flow
1. TCP 3-way handshake
2. **TLS handshake**
3. Encrypted HTTP data transmission

Even with Wireshark, encrypted data appears as gibberish unless a decryption key is provided.

> ✅ TLS protects HTTP without changing TCP or IP.

---

## 📬 Task 4 - SMTPS, POP3S, and IMAPS

TLS is added to plaintext protocols:

### 📦 Port Comparison

| Protocol | Insecure Port | Secure Port |
|----------|----------------|-------------|
| HTTP     | 80             | 443 (HTTPS) |
| SMTP     | 25             | 465/587     |
| POP3     | 110            | 995         |
| IMAP     | 143            | 993         |

> TLS adds encryption, ensuring secure communication without changing application-level syntax.

---

## 🖥️ Task 5 - SSH

![SSH with Wireshark over X11](https://github.com/user-attachments/assets/343311fb-b0d5-4fe4-b81b-1a47c71c1dbd)

**SSH (Secure Shell)** replaced Telnet for remote access.

### 🔐 SSH Benefits
- Password + public key auth
- End-to-end encryption
- Integrity checks
- Tunnel any protocol securely
- X11 GUI support (`ssh -X user@host`)

### 🔧 Usage Example
```bash
ssh username@hostname
ssh 192.168.124.148 -X  # graphical forwarding
```

OpenSSH is the most widely used open-source implementation of SSH.

---

## 📁 Task 6 - SFTP and FTPS

| Feature     | SFTP                              | FTPS                            |
|-------------|-----------------------------------|----------------------------------|
| Protocol    | Part of SSH                       | FTP + TLS                       |
| Port        | 22                                | 990                              |
| Secure      | Encrypted over SSH                | Encrypted over TLS              |
| Setup       | Simple (OpenSSH config)           | Complex (TLS cert setup needed) |

```bash
# SFTP example
sftp user@host
get filename
put filename
```

---

## 🌍 Task 7 - VPN

![VPN Branch-to-Branch](https://github.com/user-attachments/assets/3e6d893e-081a-4cde-be9a-39370a5bf929)
![VPN Remote Users](https://github.com/user-attachments/assets/c82072b5-82d9-42c5-90bc-8815149745c3)
![VPN Connection to Japan Example](https://github.com/user-attachments/assets/6843084a-6123-44d6-a54b-f13e91600368)

**VPN (Virtual Private Network)** creates a secure tunnel over the Internet.

### 🧭 Why VPN?
- Link remote offices or users
- Encrypt traffic between locations
- Hide IP and bypass censorship/geoblocks

### 📦 VPN Tunnel Features
- Blue: encrypted VPN tunnel
- Green: decrypted internal network traffic

VPN routes your traffic through the main branch. Web servers will see the VPN server's IP, not your real one.

---

## ✅ Task 8 - Closing Notes

![Wireshark TLS Setup - Step 1](https://github.com/user-attachments/assets/b0ddab6d-3deb-4043-b982-eb568301b60d)
![Wireshark TLS Setup - Step 2](https://github.com/user-attachments/assets/35210338-2ede-43c5-82a1-a31d1bfd1832)

Three secure communication approaches:

### 1. **TLS**
- Encrypts traffic between client/server
- Used for HTTPS, SMTPS, POP3S, IMAPS

### 2. **SSH**
- Secures remote terminal sessions
- File transfer and protocol tunneling

### 3. **VPN**
- Full private network over public infrastructure
- Protects entire device or site traffic

---

### 🔐 Hands-on Wireshark TLS Key Log Example

```bash
chromium --ssl-key-log-file=~/ssl-key.log
```

- Open `randy-chromium.pcapng` in Wireshark
- Load TLS key log from `Documents/ssl-key.log`
- View decrypted packets & find login credentials

---

📁 This markdown is for documentation and learning purposes only.
