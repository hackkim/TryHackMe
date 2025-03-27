# TryHackMe: OSI Model

---

## Task 1: What is the OSI Model?

![OSI 모델 다이어그램](https://github.com/user-attachments/assets/f2732d4b-3332-456a-9224-7dfdf383a585)

The **OSI model (Open Systems Interconnection Model)** is an essential framework used in networking. It defines how devices communicate over a network, allowing different devices and systems to send, receive, and interpret data uniformly.

The OSI model has **seven layers**, each with specific responsibilities, organized from **Layer 7 (Application)** down to **Layer 1 (Physical)**. 

As data moves through the layers, it undergoes **encapsulation**, where headers and information are added at each layer.

---

## Task 2: Layer 1 - Physical

![Physical Layer 이미지](https://github.com/user-attachments/assets/e78314d7-615b-4b7e-80a1-adf26fbc5e63)

This layer refers to the **hardware components** involved in data transmission. It deals with electrical signals and binary data (0s and 1s).

**Example:** Ethernet cables, switches, and hubs.

![이더넷 케이블 이미지](https://github.com/user-attachments/assets/0fb58abe-0746-4dad-a501-0885fd798aca)

---

## Task 3: Layer 2 - Data Link

![Data Link Layer 이미지](https://github.com/user-attachments/assets/cbe9dbdf-1405-41c7-899e-76cbcf025519)

The Data Link Layer is responsible for the **physical addressing** using **MAC (Media Access Control)** addresses. Each device has a unique MAC address embedded in its NIC (Network Interface Card).

It formats data for transmission and handles **frame synchronization**.

---

## Task 4: Layer 3 - Network

![Network Layer 이미지](https://github.com/user-attachments/assets/9a80a561-b131-4348-94e5-e12f7dcfc678)

This layer handles **routing** and **logical addressing** (IP addresses like 192.168.1.100). It determines the **optimal path** for data using routing protocols such as:

- **OSPF (Open Shortest Path First)**
- **RIP (Routing Information Protocol)**

**Layer 3 devices:** Routers

---

## Task 5: Layer 4 - Transport

![Transport Layer 이미지](https://github.com/user-attachments/assets/65bdb67f-9073-405b-a4e9-2315a6eef061)

This layer manages **end-to-end communication** and error checking using two protocols:

### TCP (Transmission Control Protocol)
- Ensures reliability, error checking, and proper ordering.
- Slower due to overhead.
- **Used for:** File transfer, email, web browsing.
![TCP 예시 - 패킷 순서대로 수신](https://github.com/user-attachments/assets/1bc9abd2-90ae-4cb8-8314-b38374c954a3)

| Advantages           | Disadvantages                    |
|----------------------|----------------------------------|
| Accurate and reliable| Slower and connection-heavy      |
| Order-preserving     | Cannot tolerate packet loss      |

### UDP (User Datagram Protocol)
- Faster, no error checking, no guarantee of delivery.
- **Used for:** Streaming, DNS, ARP, DHCP
![UDP 예시 - 패킷 순서대로 수신](https://github.com/user-attachments/assets/5f095314-9690-4fd3-aae6-3882d196314f)

| Advantages       | Disadvantages             |
|------------------|---------------------------|
| Fast             | No guarantee of delivery  |
| No connection overhead | Prone to packet loss |

---

## Task 6: Layer 5 - Session

![Session Layer 이미지](https://github.com/user-attachments/assets/6c5cede0-3dda-4509-82e6-fafa3c3f7a16)

This layer manages and maintains **sessions (connections)** between devices. It also handles:

- Session creation and termination
- **Checkpoints** to allow partial data resend if a session is interrupted

---

## Task 7: Layer 6 - Presentation

![Presentation Layer 이미지](https://github.com/user-attachments/assets/52c15961-d04b-43ca-817e-d22e248383f9)

Acts as a **translator** between application and network. It ensures data is presented in a usable format.

Handles:
- Data formatting
- **Encryption/Decryption** (e.g., HTTPS)
- Compression

---

## Task 8: Layer 7 - Application

![Application Layer 이미지](https://github.com/user-attachments/assets/5250efeb-a85c-4423-b261-100f2a27d40c)

This is the layer users interact with. It provides **interfaces and protocols** that allow software to communicate over the network.

**Examples:**
- Email clients
- Web browsers
- FTP software

**Common protocols:** DNS, HTTP, FTP, SMTP

---

## Task 9: Practical - OSI Game

Try the **OSI Dungeon Game**!

> Can you beat the staff high score of 19 seconds?

👉 Click the `View Site` button to play.

---

## Task 10: Continue Your Learning: Packets & Frames

Join the **"Packets and Frames"** room to learn about how data is structured into packets and frames as it moves through the OSI model.

🔗 [Go to Packets & Frames Room](https://tryhackme.com)

---
