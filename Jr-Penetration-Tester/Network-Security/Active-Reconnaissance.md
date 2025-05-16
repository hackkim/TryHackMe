# 🚀 TryHackMe: Network Security - Active Reconnaissance

This document is a comprehensive summary of the **Active Reconnaissance** portion of the TryHackMe Network Security module. Active reconnaissance involves **direct interaction** with the target environment to gather intelligence about hosts, services, and network infrastructure. Unlike passive recon, active recon can generate logs and alert defenders.

---

## 🔹 Task 1: Introduction

In this room, we shift from passive techniques to **active reconnaissance**, which involves directly connecting to a target system to obtain real-time information. These actions may trigger defensive mechanisms or leave logs (e.g., IP addresses, timestamps), so **legal authorization** is mandatory in real-world scenarios.

**Examples of active recon:**
- Pinging a server
- Accessing a web page
- Port scanning
- Connecting via Telnet or Netcat

![Passive Reconnaissance](https://github.com/user-attachments/assets/d4f0b3dd-ab22-4e16-8d7c-ec57dde84f59)
*Passive Reconnaissance — Observing from afar*

![Active Reconnaissance](https://github.com/user-attachments/assets/67f0ccf6-4d3a-48a1-9e51-4617f496443d)
*Active Reconnaissance — Interacting directly with the system*

---

## 🔹 Task 2: Web Browser

A web browser is one of the most accessible tools for reconnaissance. Modern browsers support developer tools that allow deep inspection of web applications.

**What can you do with a browser?**
- Inspect HTML/CSS/JS
- Monitor network traffic
- Observe HTTP headers and cookies
- Detect technologies in use via extensions

### Developer Tools Shortcuts:
- **Linux/Windows**: `Ctrl+Shift+I`
- **macOS**: `Option + Command + I`

![Browser Developer Tools](https://github.com/user-attachments/assets/f4f40f7c-51d4-4f61-a937-8572be22a8f3)

### 🔌 Useful Extensions:
- **FoxyProxy**: Proxy switching
- **User-Agent Switcher**: Impersonate browsers/devices
- **Wappalyzer**: Technology fingerprinting

![Wappalyzer Output](https://github.com/user-attachments/assets/a9a246e6-8abe-4f86-9190-3322cdfa0c4d)

---

## 🔹 Task 3: Ping

`ping` sends an **ICMP Echo Request** to a host and waits for a reply. It's used to:
- Check if the host is online
- Measure round-trip time (latency)

```bash
# Linux/macOS
ping -c 5 MACHINE_IP

# Windows
ping -n 5 MACHINE_IP
```

If replies are received, the host is reachable. If not:
- The host may be offline
- Firewalls may be blocking ICMP

---

## 🔹 Task 4: Traceroute

`traceroute` maps the route packets take from your machine to the target by manipulating the **TTL (Time-To-Live)** field.

Each router decrements TTL by 1:
- When TTL = 0, router drops the packet and sends an ICMP "Time Exceeded"
- This reveals the router’s IP

```bash
# Linux/macOS
traceroute tryhackme.com

# Windows
tracert tryhackme.com
```

### TTL Path Mapping:

![TTL Decrement](https://github.com/user-attachments/assets/b528a1a6-2e2f-45d0-aa2b-5e239c3cd6b0)

### ICMP Response Mechanism:

![ICMP TTL Exceeded](https://github.com/user-attachments/assets/5e94b6c3-20e6-4c3e-80dd-c63b081d1d7e)

**Real Use Cases:**
- Identifying firewall boundaries
- Understanding network layout
- Detecting filtering devices

---

## 🔹 Task 5: Telnet

`telnet` allows connection to a remote port using plain TCP. It's commonly used for banner grabbing or protocol inspection.

```bash
telnet MACHINE_IP 80
```

Then issue:
```
GET / HTTP/1.1
host: example.com
```

🛑 Telnet is insecure—credentials and data are sent in **cleartext**. Only use for testing.

---

## 🔹 Task 6: Netcat (nc)

`netcat` is a powerful tool that supports TCP/UDP connections as both **client** and **server**.

### As a client:
```bash
nc MACHINE_IP 80
GET / HTTP/1.1
host: netcat
```

### As a server:
```bash
nc -lvnp 1234
```

| Option | Description            |
|--------|------------------------|
| -l     | Listen mode            |
| -v     | Verbose output         |
| -n     | Numeric IPs (no DNS)   |
| -p     | Specify port           |
| -k     | Keep listening         |

Useful for:
- Banner grabbing
- Setting up reverse shells
- Port listening for file transfer or chat

---

## 🔹 Task 7: Putting It All Together

You can combine all previous tools into a basic manual scanning script:

| Tool     | Sample Usage                      |
|----------|-----------------------------------|
| `ping`   | `ping -c 5 MACHINE_IP`            |
| `traceroute` | `traceroute MACHINE_IP`       |
| `telnet` | `telnet MACHINE_IP PORT`          |
| `netcat` | `nc MACHINE_IP PORT`              |
| `netcat (server)` | `nc -lvnp PORT`          |

These tools help you:
- Confirm host availability
- Discover network routes
- Identify open ports and services
- Collect service banners

---

✅ **Conclusion**

Active reconnaissance is a fundamental part of penetration testing. It enables attackers (or red teamers) to map networks, identify live systems, uncover services, and prepare for exploitation. Tools like ping, traceroute, telnet, netcat, and browser dev tools form the backbone of initial network exploration.

Always remember: **get explicit permission before performing active reconnaissance.**
