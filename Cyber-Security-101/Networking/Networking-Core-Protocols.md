# 🌐 TryHackMe - Networking Core Protocols

> This markdown summarizes my learning from the **Networking Core Protocols** room on TryHackMe.  
> It is the third room in a four-part series covering key Internet protocols.

---

## 🧠 Task 1 - Introduction

![Networking Core Protocols Overview](https://github.com/user-attachments/assets/7cc4c16d-487e-4dec-96fb-a8ec1afd32d9)

This room builds upon the foundational knowledge from Networking Concepts and Essentials.

### ✅ Prerequisites
- OSI Model (7 layers)
- TCP/IP Stack
- Ethernet, IP, and TCP

### 🧾 Learning Objectives
- WHOIS
- DNS
- HTTP, FTP
- SMTP, POP3, IMAP

---

## 🌍 Task 2 - DNS: Remembering Addresses

**DNS (Domain Name System)** maps domain names to IP addresses.

### 🔹 Common DNS Record Types
| Record | Description |
|--------|-------------|
| A      | Maps domain to IPv4 |
| AAAA   | Maps domain to IPv6 |
| CNAME  | Alias to another domain |
| MX     | Mail exchange server for domain |

### 📡 Example: `nslookup`
```bash
nslookup www.example.com
```

### 📦 DNS Packet Flow (via tshark)
```bash
tshark -r dns-query.pcapng -Nn
```

- Queries sent for A and AAAA records
- Replies with IPv4 and IPv6 results

---

## 🕵️ Task 3 - WHOIS

![WHOIS Record Screenshot](https://github.com/user-attachments/assets/1fee87e7-72af-479f-a25a-490922dba805)

WHOIS reveals who owns a domain and registrar details.

### 🔍 Example: WHOIS Query
```bash
whois [domain].com
```

Fields include:
- Registrar Name and URL
- Creation/Expiration Date
- Contact Info (can be private)
- Domain Name, Name Servers

---

## 🌐 Task 4 - HTTP(S): Accessing the Web

![HTTP Web Page](https://github.com/user-attachments/assets/7c35ad83-b9e5-43fb-9aae-b5e124cc9841)
![HTTP Wireshark Stream](https://github.com/user-attachments/assets/63cace73-abd4-48f1-a9ba-7d2910b9cf39)

**HTTP (Hypertext Transfer Protocol)** allows web browsers to communicate with servers.

### 📌 Common HTTP Methods
- GET
- POST
- PUT
- DELETE

### 🔐 Ports
- HTTP: TCP 80
- HTTPS: TCP 443

### 🧪 Debugging Example
```bash
telnet MACHINE_IP 80
GET / HTTP/1.1
Host: anything
```

---

## 📁 Task 5 - FTP: Transferring Files

![FTP Wireshark Session](https://github.com/user-attachments/assets/55420b07-3ab2-4aba-ab24-8149adf1bac4)

**FTP (File Transfer Protocol)** is used for file upload/download.

### 🧰 FTP Commands
| Command | Description |
|---------|-------------|
| USER    | Username login |
| PASS    | Password login |
| RETR    | Retrieve/download |
| STOR    | Upload/store |

### 📡 FTP Session Example
```bash
ftp MACHINE_IP
USER anonymous
PASS
ls
type ascii
get coffee.txt
```

---

## 📬 Task 6 - SMTP: Sending Email

![SMTP Wireshark Session](https://github.com/user-attachments/assets/42315e93-f868-4235-b9c9-cc8e36496d01)

**SMTP (Simple Mail Transfer Protocol)** defines how email clients and servers send emails.

### ✉️ SMTP Commands
- HELO / EHLO
- MAIL FROM
- RCPT TO
- DATA
- . (to end message)

### 🔧 SMTP Session via Telnet
```bash
telnet MACHINE_IP 25
HELO client
MAIL FROM: <user@client>
RCPT TO: <receiver@server>
DATA
<message>
.
QUIT
```

---

## 📥 Task 7 - POP3: Receiving Email

![POP3 vs SMTP Mailboxes](https://github.com/user-attachments/assets/b83e6e23-20bd-47e8-ad13-48511917c362)
![POP3 Wireshark Session](https://github.com/user-attachments/assets/08e0d1ac-3603-4ef0-b732-b3e461894d36)

**POP3 (Post Office Protocol v3)** is used by mail clients to retrieve emails.

### 🔑 Common POP3 Commands
- USER
- PASS
- STAT
- LIST
- RETR <n>
- DELE <n>
- QUIT

### 🔐 Example Session
```bash
telnet MACHINE_IP 110
USER linda
PASS Pa$$123
LIST
RETR 3
QUIT
```

---

## 🔄 Task 8 - IMAP: Synchronizing Email

![IMAP Wireshark Session](https://github.com/user-attachments/assets/157bec0c-e9ae-4e46-a439-2c6f2f144e1b)

**IMAP (Internet Message Access Protocol)** allows full mailbox sync across devices.

### 📧 IMAP Commands
- LOGIN <user> <pass>
- SELECT inbox
- FETCH <n> body[]
- MOVE / COPY
- LOGOUT

### 🔗 Example
```bash
telnet MACHINE_IP 143
LOGIN user pass
SELECT inbox
FETCH 3 body[]
LOGOUT
```

---

## ✅ Task 9 - Conclusion

With the protocols covered in this room, you now have a deeper understanding of:
- Domain name resolution
- HTTP(S) request/response behavior
- FTP file transfer mechanism
- Email delivery and retrieval using SMTP, POP3, and IMAP

### 📊 Default Port Summary

| Protocol | Transport | Port |
|----------|-----------|------|
| TELNET   | TCP       | 23   |
| DNS      | UDP/TCP   | 53   |
| HTTP     | TCP       | 80   |
| HTTPS    | TCP       | 443  |
| FTP      | TCP       | 21   |
| SMTP     | TCP       | 25   |
| POP3     | TCP       | 110  |
| IMAP     | TCP       | 143  |

---

📁 This markdown is for educational and documentation purposes only.
