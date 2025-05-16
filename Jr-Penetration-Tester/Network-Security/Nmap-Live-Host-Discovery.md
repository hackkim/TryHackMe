# 🛰️ TryHackMe: Nmap Live Host Discovery

This room focuses on identifying **live hosts** before port scanning. Tools like **Nmap**, **arp-scan**, and **masscan** are used in different environments with different protocols to achieve this.

---

## 🔹 Task 1: Introduction

Before we scan for open ports, we must answer:

- **Which systems are up?**

**Nmap** is our primary tool. The scanning process usually follows these steps:

![Nmap Process Flow](https://github.com/user-attachments/assets/431d957f-4311-4294-a529-cf0e0248f5a1)

---

## 🔹 Task 2: Subnetworks

A **subnet** (subnetwork) is a logical division of an IP network.

| CIDR  | Subnet Mask     | Host Capacity |
|-------|------------------|---------------|
| /24   | 255.255.255.0    | ~250 hosts    |
| /16   | 255.255.0.0      | ~65,000 hosts |

![Subnet Topology](https://github.com/user-attachments/assets/828b1a84-a703-4871-9fd4-b4de605b80c0)

ARP scans only work within the **same subnet** due to link-layer limitations.

---

## 🔹 Task 3: Enumerating Targets

**Target formats** for Nmap:

```bash
nmap MACHINE_IP
nmap 10.11.12.15-20
nmap MACHINE_IP/30
nmap -iL targets.txt
```

Use `-sL` to list scanned hosts:
```bash
nmap -sL -n TARGETS
```

---

## 🔹 Task 4: Discovering Live Hosts (Protocols & Layers)

Host discovery can happen at various protocol layers:

| Protocol | Layer         | Used For                  |
|----------|---------------|---------------------------|
| ARP      | Link Layer    | Local subnet discovery     |
| ICMP     | Network Layer | Ping-based discovery       |
| TCP/UDP  | Transport     | Port-based host detection  |

![OSI vs TCP/IP Layers](https://github.com/user-attachments/assets/448a525d-0dd8-459a-9ade-d7a8f60da6f2)

---

## 🔹 Task 5: Nmap Host Discovery Using ARP

```bash
sudo nmap -PR -sn MACHINE_IP/24
```

ARP scan sends requests to the broadcast MAC address.

![ARP Request/Reply Flow](https://github.com/user-attachments/assets/32499967-bdd8-40ac-b6ca-4c3ab107ff3c)

**Wireshark Output:**
![Nmap ARP Traffic](https://github.com/user-attachments/assets/91e6ee46-433d-4fb4-af2b-d17c67399f95)

**arp-scan Output:**
![arp-scan ARP Broadcasts](https://github.com/user-attachments/assets/00169e12-e8e6-4373-9707-aab9fd9ce5bc)

---

## 🔹 Task 6: Nmap Host Discovery Using ICMP

### ICMP Echo
```bash
sudo nmap -PE -sn MACHINE_IP/24
```

![ICMP Echo Scan](https://github.com/user-attachments/assets/b82be884-b374-4f92-bf0f-8875c5f150f7)

![Wireshark - ICMP Echo Requests](https://github.com/user-attachments/assets/7e54b5cd-9b76-4463-84f6-49ec889b1e51)

### ICMP Timestamp
```bash
sudo nmap -PP -sn MACHINE_IP/24
```

![ICMP Timestamp Scan](https://github.com/user-attachments/assets/6f04103b-358b-4f14-aa40-cb320b56ee09)

![Wireshark - ICMP Timestamp Requests](https://github.com/user-attachments/assets/bfdc4d13-ab38-44fa-b0b0-d556efac1308)

### ICMP Address Mask
```bash
sudo nmap -PM -sn MACHINE_IP/24
```

![ICMP Address Mask Scan](https://github.com/user-attachments/assets/3390af98-b47a-4447-8576-26f1824e637d)

![Wireshark - ICMP Address Mask Requests](https://github.com/user-attachments/assets/2b7b895f-a533-4506-a567-713f4800b5c3)

---

## 🔹 Task 7: Nmap Host Discovery Using TCP and UDP

### TCP SYN Ping
```bash
sudo nmap -PS -sn MACHINE_IP/24
```

![TCP Handshake](https://github.com/user-attachments/assets/92c133c8-b87d-4a23-98b2-ca8f43d074a5)
![TCP SYN Scan Flow](https://github.com/user-attachments/assets/5c6b31fc-aec1-4d16-9a32-048f971103c7)
![Wireshark - TCP SYN Scan](https://github.com/user-attachments/assets/c2ca7814-bb44-4106-9b0c-ed9a0108b2c0)

### TCP ACK Ping
```bash
sudo nmap -PA -sn MACHINE_IP/24
```

![TCP ACK Scan Flow](https://github.com/user-attachments/assets/1cb68e05-5a6d-4914-9d66-598a6e57cbc1)
![Wireshark - TCP ACK Scan](https://github.com/user-attachments/assets/70eac432-d956-4744-a588-0a28dca579b4)

### UDP Ping
```bash
sudo nmap -PU -sn MACHINE_IP/24
```

![UDP Ping Logic](https://github.com/user-attachments/assets/c9e7d900-5996-42ac-b1bf-4f1cfd330fde)
![Wireshark - UDP Scan Output](https://github.com/user-attachments/assets/9d8a70b6-df1f-4758-8151-08d28a10624c)

---

## 🔹 Task 8: Reverse-DNS Lookup

Nmap attempts reverse DNS lookups by default.

### Options:
- `-n`: disable DNS lookup
- `-R`: reverse lookup even on offline hosts
- `--dns-servers`: specify custom DNS servers

```bash
nmap -n -sn MACHINE_IP/24
nmap -R -sn MACHINE_IP/24
```

---

## 🔹 Task 9: Summary

| Scan Type              | Command Example                                 |
|------------------------|--------------------------------------------------|
| ARP Scan               | `sudo nmap -PR -sn MACHINE_IP/24`              |
| ICMP Echo              | `sudo nmap -PE -sn MACHINE_IP/24`              |
| ICMP Timestamp         | `sudo nmap -PP -sn MACHINE_IP/24`              |
| ICMP Address Mask      | `sudo nmap -PM -sn MACHINE_IP/24`              |
| TCP SYN                | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30`     |
| TCP ACK                | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30`     |
| UDP Ping               | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30`    |

**Tips:**
- Use `-sn` to disable port scanning and focus on host discovery.
- ARP is best for local subnets.
- ICMP is useful but often blocked.
- TCP/UDP offer versatile alternatives.

---
✅ With a solid understanding of host discovery, you're now ready to move on to port scanning and service enumeration.
