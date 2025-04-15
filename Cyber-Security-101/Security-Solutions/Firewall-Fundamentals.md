# 🔥 TryHackMe - Firewall Fundamentals

> This documentation summarizes the key concepts, technologies, and hands-on activities covered in the **Firewall Fundamentals** room on TryHackMe.

---

## 🧠 Task 1 - What Is the Purpose of a Firewall

Just like a security guard filters who enters or leaves a building, a **firewall** acts as a digital gatekeeper, controlling **incoming and outgoing traffic** to or from a device or network.

### 🔍 Definition

A **firewall** is a security system—either hardware, software, or both—that monitors and controls traffic based on a set of **security rules**. It can allow or block traffic based on IP address, protocol, port, or direction.

![Firewall Concept Diagram](https://github.com/user-attachments/assets/d4e985ac-9c31-4ff6-b303-427ea41c443b)

### 🎯 Purpose

- Prevent **unauthorized access**
- Enforce **organizational policies**
- Act as a barrier between **trusted and untrusted networks**
- Log and audit network activity

---

## 🎯 Learning Objectives

By completing this room, you will understand:

- The **types of firewalls** and their OSI layer functions
- The **structure and function of firewall rules**
- How to manage firewalls in **Windows (Defender Firewall)**
- How to use **iptables/ufw in Linux**

---

## 🧱 Task 2 - Types of Firewalls

Firewall technology has evolved from simple rule-based packet filters to sophisticated security appliances. Below are four major types of firewalls:

![Types of Firewalls Diagram](https://github.com/user-attachments/assets/864e3825-41bc-4c6f-9e7b-8bf154141abf)

| 🔐 Type                 | OSI Layer(s) | Key Characteristics |
|------------------------|--------------|----------------------|
| Stateless Firewall     | L3–L4        | Matches packets against rules without remembering past connections |
| Stateful Firewall      | L3–L4        | Tracks active connections and bases decisions on traffic state |
| Proxy Firewall         | L7           | Intercepts and filters application traffic; provides anonymity |
| Next-Gen Firewall (NGFW)| L3–L7       | Combines DPI, intrusion prevention, TLS inspection, and threat intel |

### 🔄 Comparison Table

| Firewall Type        | Features |
|----------------------|----------|
| **Stateless**        | Basic rule matching, fast, no session awareness |
| **Stateful**         | Maintains session state, improved security |
| **Proxy**            | Filters content, application control, hides internal IPs |
| **Next-Gen Firewall**| DPI, heuristic analysis, IPS, SSL decryption |

---

## ⚙️ Task 3 - Rules in Firewalls

![Firewall Traffic Flow](https://github.com/user-attachments/assets/99f6b3e2-aea0-45df-beee-6543456ff279)

Firewalls rely on **rules** to make traffic control decisions.

### 🧩 Components of a Firewall Rule

- **Source Address**: IP address of the sending host
- **Destination Address**: Target IP address
- **Port**: Communication port (e.g., 80 for HTTP)
- **Protocol**: Transport protocol (TCP, UDP, etc.)
- **Direction**: Inbound, Outbound, or Forward
- **Action**: Allow / Deny / Forward

### 🔧 Example Rules

#### ✅ Allow Rule

| Action | Source        | Destination | Protocol | Port | Direction |
|--------|---------------|-------------|----------|------|-----------|
| Allow  | 192.168.1.0/24| Any         | TCP      | 80   | Outbound  |

#### ❌ Deny Rule

| Action | Source | Destination     | Protocol | Port | Direction |
|--------|--------|------------------|----------|------|-----------|
| Deny   | Any    | 192.168.1.0/24   | TCP      | 22   | Inbound   |

#### 🔁 Forward Rule

| Action  | Source | Destination   | Protocol | Port | Direction |
|---------|--------|----------------|----------|------|-----------|
| Forward | Any    | 192.168.1.8    | TCP      | 80   | Inbound   |

### 🔁 Rule Directions

- **Inbound**: Applies to incoming traffic
- **Outbound**: Applies to outgoing traffic
- **Forward**: Routes traffic from one network segment to another

---

## 🪟 Task 4 - Windows Defender Firewall


![RDP Credentials](https://github.com/user-attachments/assets/a6da9ee3-130a-47ef-be1e-09093377d92d)

![Network Profiles Overview](https://github.com/user-attachments/assets/aa8f4de1-66b9-4b2c-bf8a-3e58c8a80d36)

![Firewall Option Highlights](https://github.com/user-attachments/assets/c9ffb32d-e826-4c67-a7ab-9a4956086c86)

![TryHackMe HTTP Test Page](https://github.com/user-attachments/assets/2f1f1301-50e3-4573-9d25-12e18e0fa604)

![Advanced Settings Panel](https://github.com/user-attachments/assets/4215eb6d-f0ba-43b2-83d8-dd0445aff89e)

![New Outbound Rule - Type](https://github.com/user-attachments/assets/119b0442-2f1e-46db-ac8c-81cad5f1bd9d)

![Rule Block Action](https://github.com/user-attachments/assets/4204d74e-ce8f-4cf8-9230-a30add05fce1)

![Outbound Rule Created](https://github.com/user-attachments/assets/bd8d2323-d78f-40a3-9b2a-f7d0ae646280)

![Rule Confirmation (Flag)](https://github.com/user-attachments/assets/6f1444db-c419-41a8-a340-b5db258968e1)

![Rule Listed in Outbound Rules](https://github.com/user-attachments/assets/7929921b-a3f1-4070-9a9b-84e1491b1732)

![Final Result - HTTP Blocked](https://github.com/user-attachments/assets/41d853ba-7ce9-4ce6-ab1b-170381936544)


Windows Defender Firewall is a built-in security tool in Windows OS for traffic filtering.

### 🧭 Network Profiles

- **Private**: Home/trusted networks
- **Public**: Untrusted networks like cafes/hotspots

### 🛠️ Custom Rule Creation Example

To block HTTP/HTTPS traffic (ports 80 & 443):

1. Open **Advanced Settings**
2. Navigate to **Outbound Rules**
3. Create **New Rule** → Choose **Custom**
4. Protocol: TCP → Remote Port: `80,443`
5. Action: **Block the connection**
6. Profile: Apply to all
7. Name the rule and save

### ✅ Result

After applying, visiting websites will fail (e.g., `http://10.10.10.10`), confirming the rule works.

---


## 🐧 Task 5 - Linux iptables / ufw Firewall

Linux systems use **Netfilter** framework, managed through tools:

- **iptables**: Traditional, powerful but complex
- **nftables**: Newer replacement for iptables
- **firewalld**: Zone-based management
- **ufw**: Beginner-friendly command-line tool

### 🔧 ufw Command Examples

```bash
# Check status
sudo ufw status

# Enable firewall
sudo ufw enable

# Allow all outgoing traffic
sudo ufw default allow outgoing

# Deny incoming SSH
sudo ufw deny 22/tcp

# Show rules with index
sudo ufw status numbered

# Delete rule #2
sudo ufw delete 2
```

### 🧠 Notes

- `ufw` is a user-friendly frontend for `iptables`
- Useful for quick firewall policy testing

---

## 🧪 Task 6 - Lab Exercises

### 🔨 Windows Lab

- Create outbound rule to block HTTP/HTTPS
- Observe access denial when visiting websites

### 🔨 Linux Lab

- Use `ufw` to block/allow SSH
- Confirm rule behavior via testing

---

## ✅ Task 7 - Conclusion

You now understand:

- Types of firewalls and how they operate
- How to define and apply rules
- How to use firewall tools in Windows and Linux

---

## 📚 Further Study

- Learn `iptables` syntax for advanced Linux use
- Explore Next-Gen Firewalls (Palo Alto, FortiGate)
- Practice with **pfSense**, **OPNsense**, or **Cloud Firewalls**
