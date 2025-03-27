# TryHackMe: Packets & Frames

---

## Task 1: What are Packets and Frames

Packets and frames are small pieces of data that combine to form a complete message.  
While often discussed together, **packets** and **frames** operate at different layers in the OSI model:

- **Packets**: Exist at **Layer 3 (Network Layer)** and contain IP addresses.  
- **Frames**: Exist at **Layer 2 (Data Link Layer)** and do not include IP address information.

Think of it like an envelope inside another envelope:  
The **outer envelope** (Packet) carries the **inner envelope** (Frame), which holds the actual data.

This is part of the **encapsulation process** discussed in the OSI model.

When loading a webpage image, it’s broken into multiple packets. These packets are reassembled into the complete image on the receiving end.

![Packets example](https://github.com/user-attachments/assets/19965211-9928-4ebf-9c05-afb636a9772f)

### Packet Structure (Example: IP Packet)

| Header              | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| Time to Live (TTL)  | Prevents packets from looping forever by setting a lifespan.                |
| Checksum            | Verifies integrity of data using mathematical validation.                   |
| Source Address      | IP address of the sending device.                                           |
| Destination Address | IP address of the receiving device.                                         |

---

## Task 2: TCP/IP (The Three-Way Handshake)

**TCP (Transmission Control Protocol)** is a core network protocol that ensures reliable data transmission.

The **TCP/IP Model** has 4 layers:
- Application
- Transport
- Internet
- Network Interface

As in the OSI model, **encapsulation** occurs as data passes through each layer.

### 🔄 TCP is Connection-Based

Before transmitting data, TCP must establish a connection between the client and server.  
This is done using the **Three-Way Handshake**:

| Step | Message  | Description                                                                 |
|------|----------|-----------------------------------------------------------------------------|
| 1    | SYN      | Sent by client to start the handshake and synchronize sequence numbers.     |
| 2    | SYN/ACK  | Sent by server to acknowledge SYN and provide its own sequence number.      |
| 3    | ACK      | Sent by client to confirm receipt. Connection is now established.           |
| 4    | DATA     | Actual data is now transmitted.                                              |
| 5    | FIN      | Used to gracefully terminate the connection.                                |
| #    | RST      | Abruptly terminates the connection (used in error or failure cases).        |

![TCP Handshake Diagram](https://github.com/user-attachments/assets/7f3b6d1c-ae67-4dec-b220-3e90d2b8dc4f)

### TCP Packet Headers

| Header              | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| Source Port         | Random port chosen by sender.                                               |
| Destination Port    | Port number of the service on receiving device (e.g., 80 for HTTP).         |
| Source IP           | Sender's IP address.                                                        |
| Destination IP      | Receiver's IP address.                                                      |
| Sequence Number     | Random starting number used to reconstruct data order.                     |
| Acknowledgement No. | Confirms receipt of data using sequence + 1.                                |
| Checksum            | Validates data integrity.                                                   |
| Data                | The actual data being transmitted.                                          |
| Flag                | Controls connection behavior (e.g., SYN, ACK, FIN).                         |

### 📦 Sequence Number Example

| Device         | Initial Sequence | Acknowledged Value |
|----------------|------------------|---------------------|
| Client (Sender)| 0                | 1                   |
| Server         | 5000             | 5001                |

### 🔚 TCP Closing Process

1. Device A sends **FIN**  
2. Device B responds with **ACK + FIN**  
3. Device A responds with final **ACK**

![TCP Close Diagram](https://github.com/user-attachments/assets/2b5bcfda-b834-4555-807b-70ee0206d5e1)

---

## Task 3: Practical - Handshake

Reassemble the **TCP handshake** between Alice and Bob in the static lab and enter the flag given at the end of the conversation.

---

## Task 4: UDP/IP

**UDP (User Datagram Protocol)** is a lightweight, **stateless** protocol — it doesn’t require a connection to be established.

### 🆚 TCP vs. UDP

| Advantages of UDP              | Disadvantages of UDP                            |
|-------------------------------|--------------------------------------------------|
| Much faster than TCP          | No guarantee of delivery                         |
| More flexible for developers  | Unstable connections result in poor experience   |
| No resource reservation       | No data integrity or ordering                    |

### UDP Packet Headers

| Header              | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| Time to Live (TTL)  | Sets expiration for the packet.                                             |
| Source Address      | IP of the sending device.                                                   |
| Destination Address | IP of the receiving device.                                                 |
| Source Port         | Random port opened by sender.                                               |
| Destination Port    | Fixed port for the service on receiver (e.g., 53 for DNS).                  |
| Data                | Actual data payload.                                                        |

![UDP Connection Diagram](https://github.com/user-attachments/assets/bc67f67f-e28a-4f2a-9f45-31d34ece82f2)

---

## Task 5: Ports 101 (Practical)

Ports act like doors or docks for network communication.  
Devices use ports to send/receive data through specific services.

### 🔢 Port Range
- Total: **0 - 65535**
- **0 - 1024**: Well-known (common) ports

### 📄 Common Protocols and Ports

| Protocol       | Port | Description                                                             |
|----------------|------|-------------------------------------------------------------------------|
| FTP            | 21   | File transfer between client/server.                                    |
| SSH            | 22   | Secure command-line login.                                              |
| HTTP           | 80   | Unsecured web traffic.                                                  |
| HTTPS          | 443  | Secured web traffic (encrypted).                                        |
| SMB            | 445  | File/printer sharing on local networks.                                 |
| RDP            | 3389 | Remote desktop access with GUI.                                         |

📌 You can change the port used by services (e.g., using port 8080 instead of 80), but clients must be told explicitly (e.g., `http://site.com:8080`).

### 🧪 Practical
Connect to IP `8.8.8.8` on port `1234` to receive a flag.

---

## Task 6: Continue Your Learning: Extending Your Network

🎯 Join the final room in this module — **\"Extending Your Network\"** — to complete your learning journey!

🔗 [Go to Extending Your Network Room](https://tryhackme.com)

---
