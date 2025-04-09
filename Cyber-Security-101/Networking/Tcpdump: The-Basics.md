# 🧰 Tcpdump: The Basics - TryHackMe Room Summary

> A comprehensive and detailed walkthrough of **Tcpdump**, based on the TryHackMe room.  
> Ideal for learners who want to explore command-line packet capture and analysis.

---

## 🧩 Task 1: Introduction

![Network Protocol Chemistry Lab](image/webp;base64,UklGRiINAABXRUJQVlA4WAoAAAAQAAAAUQMAHwMAQUxQSDUEAAABHKVtGzDt/29PXBQRE8BbRVphLNZ2s21vNKh6S/g6QBXspRynEqaEwRQwmAIUbjgZhCoAM3giLmFCpwIwwnsQ3p8nkGb+3RP+c0xETIBCRpKkRTi0RVrkMxiIeyoisvjPf/7zn//85z//+c9//vOf//znP//5z3/+85///Oc///nPf/7zn//85z//+c9//vOf//znP//5z3/+85///Oc///nPf/7zn//85z//+c9//vOf//znP//5z3/+85///Oc///nPf/7zn//85z//+c9//vOf//znP//5z3/+85///Oc///nPf/7zn//85z//+c9//vOf//znP//5z3/+85///Oc///nPf/7zn//85z//+c9//vOf//znP//5z3/+85///Oc///nPf/7zn//897QtOaf5VOIbfbHziGuM83kkAyVWwJ9FHNBMAYhnkQiskoB8FslAOF2sngm3AUCSO1X0TkL1t8oBWdIEpNsRUgXqcg6YGDd3iwKQJEVguXVTYTedAawBtQLJ3I5bC31Z/SBKKoCXLbkB1G0+Ypmj8wlgAbKUgVats5Wj6cbIAU1z42D1O74yLGtsUE8AFQhSpI9d5nhuUKQNWCeONzewAtCSkzQBdvXngKo9nDTT15xz6XgZKBlornUt55w7tsECsJr6GfBXfqHcBJKkx0eblKDNGs8NnmiMtwIkp6EvwCBDCxqGBui6f2K4SPppRFCGqP0Vsq+DXwGq9sOhVb3bANKVn8ogSPoG+AGoXbYdexdekOYY2fV7y6FN0rTRN7v284M75/goUGeAuAAtxSUsN1/5F/DbKkl75BjDFGMByiACJTOuXlf+tg12kzLQ7mhcvEkKIYwOzwNrHNxMV/5T43iQB0i+XcSs/rJPtrmTb3svO13r25ol2crBX7pJSgDhxhe/7/15wwPbgbkeAYpJki055yd+BZpd6fkCi0Klb992w2ayBlTgwTne7FiVgQOSC2s9QO6GVgC2Kz1r0FaGm71xgEVaGG+y5wb4i+Qbw5YrEHZCo692naeJ3TZLGX6rJT0KVMmPkvOFvk26yDf6NElWIc6drQyT6Vp/G2WnASapAXcn+hIUGb5pUrskAySnPsNPRMkX+jbpet9qt6hPwCwpAa/S/+ZcYSzJAeWIB6rX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)
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
