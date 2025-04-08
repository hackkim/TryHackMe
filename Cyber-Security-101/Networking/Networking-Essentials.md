# 🌐 TryHackMe - Networking Essentials

> This markdown summarizes my learning from the **Networking Essentials** room on TryHackMe.  
> This is the second room in a four-part series covering foundational computer networking concepts and protocols.

---

## 🧠 Task 1 - Introduction

![Networking Essentials Overview](https://github.com/user-attachments/assets/575a9d76-4c11-49c2-b9e2-66bb41c86c65)

Have you ever wondered how your device can connect to a new network and automatically configure its network settings without you doing anything?  
This room introduces protocols that help make that possible.

### 📚 Topics Covered
- Dynamic Host Configuration Protocol (DHCP)
- Address Resolution Protocol (ARP)
- Internet Control Message Protocol (ICMP)
  - Ping
  - Traceroute
- Network Address Translation (NAT)
- Routing basics

---

## 🔌 Task 2 - DHCP: Give Me My Network Settings


DHCP (Dynamic Host Configuration Protocol) is responsible for automatically assigning IP addresses and other network settings to hosts.

### ⚙️ Key Configurations Provided by DHCP:
- IP address
- Subnet mask
- Default gateway (router)
- DNS server

### 🔄 DHCP DORA Process

![DORA Steps Table](https://github.com/user-attachments/assets/1447f730-48b3-4d92-8d44-641d5a647e3e)
![DHCP Exchange Diagram](https://github.com/user-attachments/assets/32caabb7-3c80-4dfc-9a17-983f33e28724)

1. **DHCP Discover** — client broadcasts to find DHCP server
2. **DHCP Offer** — server responds with an IP lease offer
3. **DHCP Request** — client requests offered IP
4. **DHCP Acknowledge** — server confirms lease

### 📡 Packet Capture of DHCP Exchange
```bash
tshark -r DHCP-G5000.pcap -n
```
Example output shows:
- Client starts from IP 0.0.0.0 to broadcast address 255.255.255.255
- Server offers IP address to the client's MAC
- Ports used: UDP 67 (server), UDP 68 (client)


---

## 🔗 Task 3 - ARP: Bridging Layer 3 to Layer 2

ARP (Address Resolution Protocol) translates IP addresses (Layer 3) to MAC addresses (Layer 2).

### 📦 Ethernet Frame with IP Packet
- Destination MAC
- Source MAC
- Type field (IPv4)


![ARP Exchange](https://github.com/user-attachments/assets/a84deee4-d8e0-42a8-a219-1dbb2d62bc4a)
![ARP Hex View](https://github.com/user-attachments/assets/f679179d-c62c-452a-86f6-854376313fd2)

### 🔁 ARP Process
1. Device sends ARP Request (broadcast)
2. Target responds with ARP Reply

```bash
tshark -r arp.pcapng -Nn
tcpdump -r arp.pcapng -n -v
```


Note: ARP packets are encapsulated directly in Ethernet frames, **not** inside IP or UDP.

---

## 📶 Task 4 - ICMP: Troubleshooting Networks

ICMP is used for network diagnostics and error reporting.

### 🏓 Ping

![ICMP Echo Request](https://github.com/user-attachments/assets/f0702941-9da0-43d3-86dc-d813c549b665)
![ICMP Echo Reply](https://github.com/user-attachments/assets/2ee684fc-103d-430d-bdb5-70e755cff8d8)
- Sends **ICMP Echo Request (Type 8)**
- Target replies with **ICMP Echo Reply (Type 0)**

```bash
ping 192.168.11.1 -c 4
```


### 🌍 Traceroute
- Uses TTL field in IP header
- Each router that decrements TTL to 0 sends back **ICMP Time Exceeded (Type 11)**

```bash
traceroute example.com
```

Traceroute maps the path through all intermediate routers to the destination.

---

## 🧭 Task 5 - Routing

### 🖼️ Simple Routing Structure

![Routing Overview](https://github.com/user-attachments/assets/dd35277a-b953-424d-9b5d-0de7d6317a01)
![Router Mesh Topology](https://github.com/user-attachments/assets/62dbee0e-6053-46af-a8e4-5e3ae27f5cf8)

Routing determines how data is forwarded between different networks.  
Each router decides the best path based on routing protocols or static rules.

### 🧭 Routing Protocols (Overview)
| Protocol | Type | Description |
|----------|------|-------------|
| **OSPF** | Link-State | Builds full topology map; chooses shortest path |
| **EIGRP** | Hybrid (Cisco) | Combines distance vector and link-state traits |
| **BGP** | Path Vector | Used between ISPs and autonomous systems |
| **RIP** | Distance Vector | Chooses path based on hop count (max 15 hops) |

---

## 🌐 Task 6 - NAT (Network Address Translation)

NAT allows multiple devices on a private network to access the Internet using a **single public IP address**.

![NAT Address Translation Example](https://github.com/user-attachments/assets/c4c809d6-e151-4074-bdd4-d535d12a8d51)

### 🔄 How NAT Works:
- Maps private IP:port → public IP:port
- Maintains a translation table
- Enables reuse of limited IPv4 public IP space

> Example:
> - Private IP: `192.168.0.129:15401`
> - Translated to: `212.3.4.5:19273`

NAT is essential in modern networking due to IPv4 address exhaustion.

---

## ✅ Task 7 - Closing Notes

This room introduced essential networking technologies and protocols:
- DHCP automates IP configuration
- ARP maps IP to MAC addresses
- ICMP enables diagnostics like ping and traceroute
- NAT enables Internet access with limited public IPs
- Routing makes global communication possible

> ✅ These protocols form the backbone of modern TCP/IP networking.
