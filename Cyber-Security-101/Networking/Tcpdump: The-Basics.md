# 🧰 Tcpdump: The Basics - TryHackMe Room Summary

> A comprehensive and detailed walkthrough of **Tcpdump**, based on the TryHackMe room.  
> Ideal for learners who want to explore command-line packet capture and analysis.

---

## 🧩 Task 1: Introduction

![Network Protocol Chemistry Lab](https://github.com/user-attachments/assets/480d6092-d4fa-4bb7-a736-dd45af626f19)
*Visual metaphor: Tcpdump helps reveal the “chemistry” of network protocols like ARP, TCP, UDP, SYN, ACK… normally hidden beneath the surface.*


Most users never see the internal workings of network communications, such as ARP queries or TCP handshakes. Tcpdump allows us to capture live traffic, observe real-time protocol behavior, and deeply understand network operations.

### 🔧 What is Tcpdump?

- A command-line network packet analyzer.
- Built on the **libpcap** library, written in C/C++.
- Runs on Unix-like systems and available on Windows as **WinPcap**.

### 📚 Learning Goals

- Capture packets and save them for later analysis.
- Filter packets by criteria such as host, port, or protocol.
- Display packets in readable formats (ASCII, hex, etc.).

### 🧠 Recommended Prerequisites

Familiarity with:
- The TCP/IP model
- Key protocols (TCP, UDP, ICMP, IP)
- Basic terminal usage

> Suggested TryHackMe rooms: **Networking Essentials**, **Networking Concepts**, **Secure Protocols**

---

## 🛠️ Task 2: Basic Packet Capture

### ✅ Selecting an Interface

```bash
tcpdump -i ens5
tcpdump -i any    # Listen on all interfaces
```

Check interfaces:
```bash
ip a s
```

---

### 💾 Saving Captures

```bash
tcpdump -i ens5 -w traffic.pcap
```

Saves captured packets in `.pcap` format (can be opened with Wireshark).

---

### 📂 Reading from a File

```bash
tcpdump -r traffic.pcap
```

Useful for analyzing stored traffic or attacks.

---

### 🎯 Limiting Packet Count

```bash
tcpdump -i ens5 -c 10
```

Stops after capturing the specified number of packets.

---

### 🛑 Disable Name Resolution

```bash
tcpdump -n     # Avoid DNS lookups
tcpdump -nn    # Avoid both DNS and port name lookups
```

Improves speed and reduces noise.

---

### 🔍 Verbosity Levels

```bash
tcpdump -v     # Show TTL, ID, total length
tcpdump -vv    # Additional TCP options
tcpdump -vvv   # Maximum details (e.g. MPLS labels, ICMP codes)
```

---

### 🧾 Summary of Command-Line Options

| Command        | Description |
|----------------|-------------|
| `-i INTERFACE` | Select interface to capture |
| `-w FILE`      | Write packets to a .pcap file |
| `-r FILE`      | Read packets from file |
| `-c COUNT`     | Stop after N packets |
| `-n` / `-nn`   | Disable hostname / service name resolution |
| `-v` / `-vv` / `-vvv` | Increase verbosity level |

---

## 🎯 Task 3: Filtering Expressions

![Filtering Concept](https://github.com/user-attachments/assets/29437e3e-3021-4c5e-9021-89a0a9881c8c)
*Illustration: Filtering expressions in Tcpdump work like a digital filter — pouring raw traffic through specific rules to isolate what matters.*


### 🎯 Filter by Host

```bash
tcpdump host 1.1.1.1
tcpdump src host 192.168.1.10
tcpdump dst host example.com
```

---

### 🔢 Filter by Port

```bash
tcpdump port 80
tcpdump src port 443
tcpdump dst port 22
```

---

### 🌐 Filter by Protocol

```bash
tcpdump tcp
tcpdump udp
tcpdump icmp
```

---

### 🔗 Combine with Logical Operators

```bash
tcpdump host 1.1.1.1 and tcp
tcpdump udp or icmp
tcpdump not tcp
```

---

### 📊 Example: Count Matching Packets

```bash
tcpdump -r traffic.pcap src host 192.168.124.1 -n | wc -l
```

---

## 🧠 Task 4: Advanced Filtering

![Advanced Protocol Analysis](https://github.com/user-attachments/assets/20a244cb-a894-4597-bfee-53ce9160db80)
*Visual metaphor: Advanced filtering in Tcpdump is like isolating specific chemical reactions — precise, layered, and requiring deep understanding of the “molecular structure” of packets.*


### 📏 Packet Size Filters

```bash
tcpdump greater 100
tcpdump less 50
```

---

### 🧮 Header Byte Filtering with Binary Operations

```bash
tcpdump 'ether[0] & 1 != 0'   # Multicast MAC
tcpdump 'ip[0] & 0xf != 5'    # IP header with options
```

Syntax:
```
proto[expr:size]
```
- `proto`: Protocol (e.g., ether, ip, tcp)
- `expr`: Byte offset
- `size`: Number of bytes (optional)

---

### 🚩 TCP Flags Filtering

| Flag     | Description |
|----------|-------------|
| `tcp-syn`  | SYN (connection start) |
| `tcp-ack`  | ACK (acknowledgment) |
| `tcp-fin`  | FIN (connection end) |
| `tcp-rst`  | RST (reset connection) |
| `tcp-push` | PSH (push data now) |

Examples:

```bash
tcpdump "tcp[tcpflags] == tcp-syn"
tcpdump "tcp[tcpflags] & tcp-syn != 0"
tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"
```

---

## 🖥️ Task 5: Displaying Packets

### 🧾 Display Format Options

| Option | Description |
|--------|-------------|
| `-q`   | Quick summary |
| `-e`   | Show Ethernet (MAC) headers |
| `-A`   | Print payload in ASCII |
| `-xx`  | Hexadecimal dump |
| `-X`   | Hex + ASCII together |

---

### 🧪 Display Examples

```bash
tcpdump -r file.pcap -q     # Quick info
tcpdump -r file.pcap -e     # Show MACs
tcpdump -r file.pcap -A     # ASCII format
tcpdump -r file.pcap -xx    # Hex only
tcpdump -r file.pcap -X     # Hex + ASCII
```

---

## ✅ Task 6: Conclusion

Tcpdump is a powerful, lightweight network analyzer for packet capture and CLI-level inspection.  
With precise filtering, binary flag matching, and advanced display options, it becomes an essential tool for:

- 🛡️ Network forensics
- 🧪 Protocol learning
- 🧠 Red teaming & threat hunting

> For deeper inspection, pair Tcpdump with **Wireshark** or **TShark**.

---

_📘 Created by: Kim Sunghoon_  
_For professional use in network security, red teaming, and analysis_
