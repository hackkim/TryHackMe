# 📡 TryHackMe: Network Security - Protocols and Servers

This document explores foundational network protocols including Telnet, HTTP, FTP, SMTP, POP3, and IMAP, providing insight into how they operate at a low level and revealing associated security concerns.

---

## ✅ Task 1 - Introduction

In this room, we explore how the following protocols work under the hood:

- HTTP
- FTP
- POP3
- SMTP
- IMAP
- Telnet

Using tools like **Telnet**, we interact directly with these services to see how clients (usually GUI-based) actually communicate with servers. This hands-on interaction makes it easier to understand the protocols’ mechanics and **security flaws**—especially how **many of them transmit sensitive data in cleartext**.

---

## 🔐 Task 2 - Telnet

**Telnet** is an **application-layer protocol** used for remote login. It connects to servers (usually on **TCP port 23**) and provides command-line access.

- **No encryption**: All data, including passwords, are sent in cleartext.
- **Modern alternative**: SSH.

Example:

```bash
telnet MACHINE_IP
```

You'll see prompts for a username and password. Below is a capture using Wireshark that shows the password was sent in cleartext:

![Telnet Password Leak](https://github.com/user-attachments/assets/8585c3c1-8981-4833-9435-92beb2e0a528)

---

## 🌐 Task 3 - HTTP (Hypertext Transfer Protocol)

**HTTP** allows web browsers to fetch resources from a server, like HTML files or images. It communicates over **TCP port 80**.

Key points:

- Commands like `GET /index.html HTTP/1.1` are used.
- Like Telnet, HTTP is **cleartext**, so anyone intercepting traffic can read the content.

Example interaction:

```bash
telnet MACHINE_IP 80
GET /index.html HTTP/1.1
host: telnet
```

Result:

- You receive HTTP headers and HTML content.
- Server type can often be inferred from headers.

Diagram:

![HTTP Request and Response Flow](https://github.com/user-attachments/assets/a3a7659c-19d3-49c0-9590-b66f47e18ad6)

Popular servers: Apache, Nginx, IIS  
Popular clients: Chrome, Firefox, Edge, Safari

---

## 📁 Task 4 - FTP (File Transfer Protocol)

**FTP** is used to transfer files between computers. It uses:

- **TCP port 21** for control
- **TCP port 20** for active-mode data transfer

Like Telnet and HTTP, FTP is **insecure** due to cleartext credentials.

Example Telnet login:

```bash
telnet MACHINE_IP 21
USER frank
PASS D2xc9CgD
```

Example client interaction:

```bash
ftp MACHINE_IP
ls
ascii
get README.txt
```

FTP diagram:

![FTP Control and Data Channels](https://github.com/user-attachments/assets/a36372ce-785e-4d06-859e-056dba0b8ba2)

FTP servers: vsftpd, ProFTPD  
FTP clients: FileZilla, CLI `ftp`

---

## ✉️ Task 5 - SMTP (Simple Mail Transfer Protocol)

**SMTP** is used for **sending** emails between servers and from clients to servers. It operates over **TCP port 25**.

Communication path:

1. MUA ➝ MSA ➝ MTA ➝ MDA ➝ MUA

Example interaction:

```bash
telnet MACHINE_IP 25
helo telnet
mail from:<sender@example.com>
rcpt to:<receiver@example.com>
data
Subject: Hello
Hello, Frank.
.
```

SMTP architecture:

![SMTP Email Delivery Flow](https://github.com/user-attachments/assets/7701954a-80bf-4eb1-9229-b599a32a798b)

---

## 📥 Task 6 - POP3 (Post Office Protocol v3)

**POP3** is used to **retrieve** emails from a Mail Delivery Agent (MDA). It connects over **TCP port 110**.

- Email is usually **downloaded and deleted**.
- Commands: `USER`, `PASS`, `STAT`, `LIST`, `RETR`

Telnet example:

```bash
telnet MACHINE_IP 110
USER frank
PASS D2xc9CgD
LIST
RETR 1
QUIT
```

Diagram:

![POP3 or IMAP Email Retrieval](https://github.com/user-attachments/assets/223743ba-ba2b-4517-9894-09692b3ba09e)

---

## 🔄 Task 7 - IMAP (Internet Message Access Protocol)

**IMAP** is a more advanced protocol than POP3, allowing clients to:

- **Synchronize emails** across multiple devices.
- **Manage folders** and retain email status.

- **TCP port**: 143

Telnet interaction with IMAP:

```bash
telnet MACHINE_IP 143
c1 LOGIN frank D2xc9CgD
c2 LIST "" "*"
c3 EXAMINE INBOX
c4 LOGOUT
```

- Commands are prefixed (`c1`, `c2`, etc.) for tracking responses.

---

## 🧾 Task 8 - Summary Table

Here is a summary of the protocols covered:

| Protocol | TCP Port | Purpose               | Security   |
|----------|----------|------------------------|------------|
| Telnet   | 23       | Remote access          | ❌ Cleartext |
| HTTP     | 80       | Web browsing           | ❌ Cleartext |
| FTP      | 21       | File transfer          | ❌ Cleartext |
| SMTP     | 25       | Sending email          | ❌ Cleartext |
| POP3     | 110      | Retrieving email       | ❌ Cleartext |
| IMAP     | 143      | Email synchronization  | ❌ Cleartext |

---

## 🚀 What’s Next?

In the following room, you will learn about **attacks targeting these protocols** and how to **harden services** against common threats like:

- Credential sniffing
- Packet manipulation
- Man-in-the-middle attacks (MITM)

Stay tuned!
