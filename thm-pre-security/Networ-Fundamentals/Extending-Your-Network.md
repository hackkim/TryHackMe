# TryHackMe: Extending Your Network

---

## Task 1: Introduction to Port Forwarding

Port forwarding allows internal services (like web servers) to be accessible from external networks (like the internet). Without port forwarding, only devices in the same local network (intranet) can access them.

For example, in the diagram below, only internal computers can reach the web server at `192.168.1.10:80`:

![Intranet Web Server](https://github.com/user-attachments/assets/27edf39c-aeef-46cc-9299-5fb4b371dd97)

To allow access from the internet, the administrator configures port forwarding:

![Internet Port Forwarding](https://github.com/user-attachments/assets/9b1b7ebc-399f-438d-9c4d-5980ea0e22c2)

Now, devices in Network #2 can access the web server using the public IP `82.62.51.70`.

> ✅ Port forwarding opens specific ports on the router.  
> 🔐 Firewalls (covered next) control whether traffic can pass through those ports.

---

## Task 2: Firewalls 101

A **firewall** monitors and filters traffic entering or leaving a network. Think of it as digital border security.

Firewalls allow or deny traffic based on:
- Source and destination IP addresses
- Port numbers (e.g., port 80 for web)
- Protocol (TCP/UDP)

![Firewall Concept](https://github.com/user-attachments/assets/1da8f791-57ad-4191-b633-cb8d93170236)

### 🔥 Firewall Types

| Type      | Description |
|-----------|-------------|
| **Stateful** | Tracks entire connections. Uses more resources but makes dynamic decisions. Can block devices based on connection behavior. |
| **Stateless** | Uses predefined rules per packet. Lighter and faster, but less intelligent. Effective for detecting high-volume attacks like DDoS. |

---

## Task 3: Practical - Firewall

🛠️ Launch the static site. Identify red (malicious) packets on port 80 and block them from reaching web server `203.0.110.1`.

---

## Task 4: VPN Basics

A **Virtual Private Network (VPN)** creates a secure tunnel over the internet, linking devices into a private network.

### Example

- Network #1: Office 1  
- Network #2: Office 2  
- Network #3: VPN between devices on Networks 1 & 2

![VPN Diagram](https://github.com/user-attachments/assets/f419a11a-85d9-45fc-aeeb-39ab668b48f6)

### ✅ VPN Benefits

| Benefit        | Description |
|----------------|-------------|
| Remote Access  | Connect offices across locations to share resources. |
| Privacy        | Encrypts traffic to prevent eavesdropping (especially on public WiFi). |
| Anonymity      | Hides user identity. Often used by journalists and activists. |
| Security       | TryHackMe uses VPN to isolate vulnerable machines from the internet. |

### 📡 VPN Technologies

| Technology | Description |
|------------|-------------|
| **PPP**    | Used for encryption/authentication. Forms the basis of other VPN protocols. |
| **PPTP**   | Easy to set up but weaker encryption. Works over PPP. |
| **IPSec**  | Strong encryption over IP. Complex to set up but highly secure. |

---

## Task 5: LAN Networking Devices

### 🛣️ What is a Router?

Routers connect different networks and direct data between them (Layer 3 of OSI). They determine optimal paths based on speed, reliability, and hops.

![Router Path Example](https://github.com/user-attachments/assets/477f2520-e702-4e89-938f-edaf3f0e60fb)

> Routers are not the same as switches.

---

### 🔌 What is a Switch?

**Switches** connect multiple devices on the same local network.

- **Layer 2 switches** use MAC addresses to forward frames.
- **Layer 3 switches** can also route packets like routers.

![Layer 2 Switch](https://github.com/user-attachments/assets/d9fca9c1-3a93-4263-b69d-c51b132b2c06)

### 🧠 VLAN (Virtual LAN)

VLANs segment a network into separate virtual groups for security and control.

![VLAN Diagram](https://github.com/user-attachments/assets/ad75c1af-8232-48f0-a75e-d4e1d06ec910)

> Devices in different VLANs can’t directly talk, even if on the same switch.

---

## Task 6: Practical - Network Simulator

Launch the simulator to trace how packets move between devices.

🔍 Try sending a **TCP packet from computer1 to computer3** to reveal the flag.

> 🧪 Use **Chrome or Firefox** for best experience.
