# 🔍 Nmap: The Basics – TryHackMe Room Summary

> A comprehensive guide to the fundamentals of Nmap.  
> Learn how to discover hosts, enumerate services, scan ports, detect versions, adjust timing, and export results effectively.

---

## 🧩 Task 1: Introduction

![Radar Scan Concept](https://github.com/user-attachments/assets/f828c456-55f6-4b6f-a17e-8a0546cf11b7)
*Visual metaphor: Nmap acts like a digital radar — identifying and sweeping across networks to find active hosts and services.*


### 🧠 Problem Overview

In a networked environment, two key reconnaissance questions often arise:

1. **Which devices are online (live hosts)?**
2. **Which services are running on those hosts?**

Manual tools like `ping`, `telnet`, or `arp-scan` are limited:
- Firewalls may block ICMP or ARP
- Scripts using Telnet to brute-force ports are inefficient
- Scanning thousands of hosts/services manually is impractical

---

### 🚀 Solution: Nmap

**Nmap (Network Mapper)** is a powerful, flexible, and open-source network scanner.  
It allows penetration testers, sysadmins, and security professionals to:

- Discover live hosts on a network
- Identify open TCP/UDP ports
- Enumerate running services and versions
- Detect operating systems
- Adjust timing and stealthiness
- Format and export scan results

> 📅 First released in 1997, Nmap has become the industry standard for network mapping and enumeration.

---

## 📡 Task 2: Host Discovery – Who Is Online?

![Server Discovery Concept](https://github.com/user-attachments/assets/a11ba95c-f203-404c-b0de-d072546b192e)

*A metaphor for Nmap host discovery: a laptop probing racks of unknown systems to identify which are active.*

![Wireshark Capture of Nmap Ping Scan](https://github.com/user-attachments/assets/9b47774f-888e-4cb9-a288-155bcb906c8f)
*This Wireshark capture shows ICMP echo requests and destination unreachable replies when using `nmap -sn` to discover hosts on a remote network.*


### 🎯 Basic Host Discovery (Ping Scan)

```bash
nmap -sn 192.168.0.1/24
```
- Sends ICMP Echo Requests, ARP Requests (on local LAN), and TCP SYN/ACK or Timestamp probes.
- Used to determine which hosts are "up".

### 🔄 Target Format Options

| Format | Description |
|--------|-------------|
| `192.168.0.1-10` | Scan a range |
| `192.168.0.1/24` | CIDR notation |
| `example.com`    | Hostname resolution |

### 🖧 Local vs Remote

- Local networks (e.g., `WiFi`) use **ARP requests** for discovery.
- Remote networks (through routers) use **ICMP/TCP** based techniques.

---

### 📃 List Scan

```bash
nmap -sL 192.168.0.0/24
```
- Lists hosts that **would be scanned**, without sending any probes.

---

## 🧪 Task 3: Port Scanning – Who Is Listening?

![Service Discovery Concept](https://github.com/user-attachments/assets/a72c791f-337d-41cc-9f7e-2af9dd03be48)
*A conceptual illustration of probing a target system to identify open services and exposed ports.*

![Connect Scan Packet Capture](https://github.com/user-attachments/assets/4e94dbc0-0542-4fea-b6d5-8e5b20b7b931)
*Wireshark capture showing TCP 3-way handshake for port 22 (open) and RST for port 23 (closed) – typical of Nmap `-sT`.*

![SYN Scan Packet Capture](https://github.com/user-attachments/assets/20cc0bfd-7a96-4fc0-b3a6-338b7e889f25)
*SYN scan (`-sS`) does not complete the handshake. Nmap sends a SYN and responds to SYN-ACK with RST, remaining stealthy.*

![UDP Scan Packet Capture](https://github.com/user-attachments/assets/4402b840-3629-4bdf-bd85-2b7981e44033)
*UDP scan (`-sU`) shows multiple ICMP "port unreachable" messages, indicating closed ports.*


### 🚪 TCP Port Scanning

#### 📍 Connect Scan (`-sT`)
```bash
nmap -sT 192.168.1.1
```
- Completes full **TCP handshake**
- Detectable in server logs
- Default method for **non-root** users

#### 🕵️ SYN Scan (Stealth, `-sS`)
```bash
nmap -sS 192.168.1.1
```
- Sends SYN only, expects SYN-ACK → resets
- Quieter than connect scan
- **Default for root** users

---

### 🔀 UDP Port Scanning

```bash
nmap -sU 192.168.1.1
```
- Slower due to lack of handshake
- Looks for **ICMP port unreachable** errors to infer closed ports

---

### 🎯 Port Range Specification

| Command        | Description |
|----------------|-------------|
| `-F`           | Fast scan (top 100 ports) |
| `-p1-1024`     | Custom range |
| `-p-25`        | Ports 1–25 |
| `-p-`          | All 65535 ports |

---

## 🧠 Task 4: Version & OS Detection

![Version & OS Detection](https://github.com/user-attachments/assets/165c3ed7-f901-48c3-ac9a-416766d6470a)
*A visual representation of fingerprinting and analysis — Nmap leverages banner grabbing, TCP/IP stack quirks, and other signals to detect services and OS types.*


### 🎯 OS Detection (`-O`)

```bash
nmap -O 192.168.1.1
```
- Passive fingerprinting using TCP/IP stack behavior
- Accuracy depends on system responses

---

### 🔍 Version Detection (`-sV`)

```bash
nmap -sV 192.168.1.1
```
- Identifies service software and version
- Helps detect misconfigured or vulnerable services

---

### 🧩 Aggressive Scan (`-A`)

```bash
nmap -A 192.168.1.1
```
Includes:
- OS detection
- Version scan
- Traceroute
- Script scanning

---

### 🔄 Force Scan All Hosts (`-Pn`)

```bash
nmap -Pn 192.168.1.1
```
- Treats all hosts as **up**, even if they don’t respond to pings

---

## ⏱️ Task 5: Timing & Performance Tuning

![Scan Speed Visualization](https://github.com/user-attachments/assets/4d9a4668-4f96-4fd3-b616-6f90017a6d6e)
*A metaphorical representation of scan speed — selecting a timing template is like choosing the thrust of a reconnaissance rocket.*

![Wireshark Capture - T0 Timing](https://github.com/user-attachments/assets/4040e707-67d6-40d9-9a98-4fd0719d0782)
*With `-T0` (paranoid), packets are spaced out by hundreds of seconds to evade IDS.*

![Wireshark Capture - T1 Timing](https://github.com/user-attachments/assets/bb670ec9-0758-4513-bcd0-be3bfda34465)
*With `-T1` (sneaky), there’s a deliberate pause between each probe — good for stealth scanning.*

![Wireshark Capture - T2 Timing](https://github.com/user-attachments/assets/694eccb5-c5c3-4f63-ad0f-61616fd33dca)
*At `-T2` (polite), spacing is shortened but still conservative.*

![Wireshark Capture - T3 Timing](https://github.com/user-attachments/assets/e21a2274-b54e-4d11-b0e0-3cd155788519)
*With `-T3` (normal), Nmap sends packets quickly in typical network conditions.*


### ⚙️ Timing Templates

```bash
-T0  # Paranoid (slowest, avoids IDS)
-T1  # Sneaky
-T2  # Polite
-T3  # Normal (default)
-T4  # Aggressive (faster)
-T5  # Insane (fastest)
```

---

### 📊 Advanced Scan Control

| Option | Function |
|--------|----------|
| `--min-parallelism N` | Minimum probes per host |
| `--max-parallelism N` | Maximum parallel probes |
| `--min-rate N`        | Min packets per second |
| `--max-rate N`        | Max packets per second |
| `--host-timeout T`    | Limit time per host |

---

## 🖥️ Task 6: Output – Control and Reporting

### 📣 Real-Time Feedback

```bash
-v, -vv, -v3, -v4   # Verbose output
-d, -dd, -d9        # Debug levels (very detailed)
```

> Use verbosity to see scan stages: ping sweep, DNS resolution, port scan, etc.

---

### 🧾 Saving Scan Results

```bash
-oN file.txt     # Normal output
-oX file.xml     # XML format
-oG file.gnmap   # Grepable output
-oA base         # Save in all 3 formats (creates .nmap, .gnmap, .xml)
```

Example:
```bash
nmap -sS 192.168.1.1 -oA result
```

---

## ✅ Task 7: Final Summary

### 📘 Option Review Table

| Category | Option | Description |
|----------|--------|-------------|
| 🎯 Host Discovery | `-sn` | Ping scan only |
| 📋 Target Listing | `-sL` | List without scanning |
| 🔍 Port Scanning | `-sT`, `-sS`, `-sU`, `-F`, `-p-` | TCP, UDP, port control |
| 💻 OS & Service | `-O`, `-sV`, `-A` | OS fingerprinting, version detection |
| 📡 Timing | `-T0`–`T5`, `--min/max-rate`, `--min/max-parallelism`, `--host-timeout` | Speed control |
| 📤 Output | `-v`, `-vv`, `-v3`, `-d`, `-d9` | Feedback levels |
| 💾 Reporting | `-oN`, `-oX`, `-oG`, `-oA` | File outputs |
| 🧱 Force Scan | `-Pn` | Assume host is up |

---

📌 **Tip**: Run `Nmap` with `sudo` to unlock raw socket functionality and enable stealth scanning (`-sS`, etc.).

---

📘 _Created by: Kim Sunghoon_  
_For efficient use in reconnaissance, network analysis, and pentesting workflows_
