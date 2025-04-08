# 📡 TryHackMe - Networking Concepts

> This document is a detailed summary of the **Networking Concepts** room from TryHackMe.  
> It is part of a series of networking modules, and builds foundational understanding of network models, protocols, addressing, and communication.

---

## 🧠 Task 1 - Introduction

![Networking Overview](https://github.com/user-attachments/assets/fd14f1cc-96c6-4d80-9d40-e0d719562ff7)

Have you ever wondered how the internet works at a technical level? This room introduces fundamental networking concepts including:

- OSI Model
- TCP/IP Model
- IP Addressing and Subnets
- UDP vs TCP
- Packet Encapsulation
- Using Telnet to test connections

> **Part of a 4-room series:**
> - Networking Concepts
> - Networking Essentials
> - Networking Core Protocols
> - Networking Secure Protocols

---

## 🧱 Task 2 - OSI Model
---

## 🔍 Full OSI 7-Layer Explanation

The OSI model is a standard reference model that divides network communication into 7 layers. Each layer has a specific role and uses a process called 'encapsulation' to transmit data from top to bottom.

### 📊 Layer-by-Layer Explanation

#### 🔸 Layer 7 - Application Layer
- **Role**: Closest to the user; allows applications to interact with network services.
- **Protocols**: HTTP, FTP, SMTP, DNS, Telnet
- **Attack Example**: Web attacks (XSS, SQL injection), Phishing

#### 🔸 Layer 6 - Presentation Layer
- **Role**: Handles data format translation, encoding/decoding, compression, and encryption.
- **Examples**: SSL/TLS encryption, JPEG/PNG formats, ASCII/Unicode encoding

#### 🔸 Layer 5 - Session Layer
- **Role**: Establishes, manages, and terminates communication sessions; handles authentication and session state.
- **Examples**: RPC, SMB sessions

#### 🔸 Layer 4 - Transport Layer
- **Role**: Provides reliable, end-to-end communication between devices using ports.
- **Protocols**: TCP, UDP
- **Attack Example**: TCP session hijacking, Port scanning

#### 🔸 Layer 3 - Network Layer
- **Role**: Routes data between different networks using logical addressing (IP).
- **Protocols**: IP, ICMP, IPSec
- **Attack Example**: IP spoofing, ICMP flood

#### 🔸 Layer 2 - Data Link Layer
- **Role**: Ensures data transfer between devices on the same network using MAC addresses.
- **Technologies**: Ethernet, ARP, Wi-Fi
- **Attack Example**: ARP spoofing, MAC flooding

#### 🔸 Layer 1 - Physical Layer
- **Role**: Transmits raw binary data (bits) over a physical medium such as electrical, optical, or wireless signals.
- **Devices**: Cables, Repeaters, Hubs
- **Attack Example**: Physical device tampering, Wiretapping (TAP devices)

### 📋 OSI Full Summary Table

| Layer | Name             | Main Function                                | Protocols/Technologies                   |
|------|------------------|-------------------------------------------|--------------------------------|
| 7    | Application      | User Application & Network Interface | HTTP, DNS, FTP, Telnet        |
| 6    | Presentation     | Data Formatting, Encryption             | SSL/TLS, JPEG, ASCII, MIME    |
| 5    | Session          | Session Setup/Maintenance/Termination                      | RPC, NetBIOS, SMB             |
| 4    | Transport        | End-to-End Communication, Port, Reliability           | TCP, UDP                      |
| 3    | Network          | IP-Based Routing                       | IP, ICMP, IPSec               |
| 2    | Data Link        | MAC-Based Transmission, Error Detection             | Ethernet, ARP, 802.3, 802.11  |
| 1    | Physical         | Bit Transmission (Electrical/Optical/Wireless)             | Cables, Wireless, Hubs, Repeaters     |


The OSI model is a theoretical framework that defines how data communication happens in seven layers:

1. Physical Layer
2. Data Link Layer
3. Network Layer
4. Transport Layer
5. Session Layer
6. Presentation Layer
7. Application Layer

### 🖼️ Layer Visuals

![OSI 7 Layers Color](https://github.com/user-attachments/assets/938e0d5a-d27c-4e8d-9910-cfd1634d2bc3)
![Physical Layer - Cables](https://github.com/user-attachments/assets/a1db4522-f577-4f16-9a3b-f504b129be4e)
![MAC Address Breakdown](https://github.com/user-attachments/assets/b8c8e930-82a7-42e8-8bae-b0edb31b9bf2)
![Wireshark Frame Capture](https://github.com/user-attachments/assets/2c2d1616-532e-42a2-b64a-f6883755c184)
![Network Layer Routing](https://github.com/user-attachments/assets/0ef6b834-3edd-4e1f-8efe-9c8cf793b29d)
---

## 🧱 Task 3 - TCP/IP Model

Unlike the OSI model, the TCP/IP model is practical and used in real-world networking. It maps roughly to OSI as follows:

| OSI Layer            | TCP/IP Layer        | Example Protocols                     |
|----------------------|---------------------|---------------------------------------|
| Application (5-7)    | Application Layer    | HTTP, HTTPS, FTP, SMTP, DNS, Telnet   |
| Transport (4)        | Transport Layer      | TCP, UDP                              |
| Network (3)          | Internet Layer       | IP, ICMP, IPSec                       |
| Data Link + Physical | Link Layer           | Ethernet, WiFi                        |

Modern textbooks may show a 5-layer stack including a separate physical layer.

---

## 🌐 Task 4 - IP Addresses and Subnets

- IPv4 consists of **4 octets** (32 bits) — e.g., `192.168.1.1`
- Special addresses:
  - Network: `.0` (e.g., `192.168.1.0`)
  - Broadcast: `.255` (e.g., `192.168.1.255`)

### 🔒 Private IP Ranges (RFC 1918)
- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

### 🔍 Commands to Check IP
```bash
ifconfig
ip a s
```

![IPv4 Octet Breakdown](https://github.com/user-attachments/assets/76bcffb5-c017-4779-8f60-239dbe65deca)

> Subnet mask `255.255.255.0` = `/24` CIDR notation → 256 total addresses

### 📦 Routing
A router works like a post office:
- Examines destination IP
- Forwards packets to the appropriate next hop

![Network Routing Topology](https://github.com/user-attachments/assets/ac4ea038-7b28-42a2-bf51-4cafb169cef6)

---

## 🔄 Task 5 - UDP and TCP

### 🚀 UDP (User Datagram Protocol)
- **Connectionless**, fast, no delivery guarantee
- Port numbers range: `1–65535`

🟨 Like regular mail — fast, but no confirmation.

### 🔁 TCP (Transmission Control Protocol)
- **Connection-oriented**, reliable
- Ensures ordered delivery via **3-way handshake**

**3-Way Handshake:**
1. SYN
2. SYN-ACK
3. ACK

![TCP 3-Way Handshake Visual](https://github.com/user-attachments/assets/54ce757f-dd15-4a63-9613-7784cb9e05a5)

---

## 📦 Task 6 - Encapsulation

Each network layer **adds a header** to the data as it passes down the stack:

1. Application → data
2. Transport → segment
3. Internet → packet
4. Link → frame


![Encapsulation Layers](https://github.com/user-attachments/assets/82be3c9b-f7f5-46ae-8ac2-db37d38165d1)



> On the receiving end, each layer **removes** its header and passes the data up the stack.

---

## 📡 Task 7 - Telnet

The **Telnet protocol** lets us manually connect to TCP ports to test connectivity.

### 🧪 Echo Server (Port 7)
```bash
telnet MACHINE_IP 7
Hi
Hi
Bye
Bye
```

### 🕒 Daytime Server (Port 13)
```bash
telnet MACHINE_IP 13
Thu Jun 20 12:36:32 PM UTC 2024
```

### 🌍 HTTP Server (Port 80)
```bash
telnet MACHINE_IP 80
GET / HTTP/1.1
Host: telnet.thm
```

You must press `Enter` twice after typing to receive the response.

---

## ✅ Task 8 - Conclusion

### 🧾 You Learned:
- OSI vs TCP/IP Models
- IP Addressing and Routing
- TCP vs UDP and their mechanisms
- Encapsulation and how data moves in layers
- Real use of Telnet to test TCP ports

> 📘 Now move on to **Networking Essentials** for deeper protocol study!

---

📁 All content in this repo is for educational purposes only.  
🔐 No flags, solutions, or proprietary material from TryHackMe is included.

