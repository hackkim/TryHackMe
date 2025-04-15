# 🛡️ TryHackMe - IDS Fundamentals

> This markdown provides a detailed summary of the **IDS Fundamentals** room on TryHackMe.  
> It explains the core concepts of Intrusion Detection Systems (IDS), types of IDS, detection methodologies, and usage of Snort as an open-source IDS.

---

## 🧠 Task 1 - What Is an IDS?

A **Firewall** filters traffic at the network boundary based on rules before connections are established. However, if a malicious actor bypasses the firewall and initiates an attack **inside** the network, a new layer of defense is needed.

That defense is provided by an **Intrusion Detection System (IDS)**.

### 🔐 IDS vs Firewall (Analogy)

- **Firewall**: Security guard at the entrance.
- **IDS**: Surveillance camera monitoring activity inside the building.

### 🧩 IDS Functionality

- **Monitors** internal and inbound/outbound traffic
- **Detects** known and unknown threats
- **Alerts** administrators (does not block by default)

---

![Firewall Bypass to IDS Concept](https://github.com/user-attachments/assets/42930848-cfb9-4b2a-b461-481463658830)

## 🎯 Learning Objectives

- Understand the **different types** and deployment models of IDS
- Learn **Snort IDS architecture** and detection modes
- Create and test **Snort custom rules**
- Use Snort to analyze **live traffic** and **PCAP files**

---

## 🧱 Task 2 - Types of IDS

![HIDS vs NIDS Architecture](https://github.com/user-attachments/assets/8e9c5519-c5bd-4d22-8b78-49729703a3b6)

IDS solutions are categorized by **deployment model** and **detection methodology**.

### 🖥 Deployment Models

| Type | Description | Pros | Cons |
|------|-------------|------|------|
| **HIDS** | Installed on individual hosts | High visibility into local activities | High overhead on large networks |
| **NIDS** | Monitors network traffic centrally | Broad visibility across network | May miss host-specific activities |

---

### 📡 Detection Modes

| Type | Description | Pros | Cons |
|------|-------------|------|------|
| **Signature-Based** | Matches traffic to known attack patterns | Fast, accurate for known threats | Can’t detect zero-day attacks |
| **Anomaly-Based** | Detects deviations from normal behavior | Detects unknown/zero-day threats | High false positive rate |
| **Hybrid** | Combines signature and anomaly detection | Flexible, broader coverage | Complex to configure and manage |

### 💬 Use Case Summary

- Use **Signature-based IDS** for well-known threats and low resource usage
- Use **Anomaly-based IDS** for dynamic environments where zero-day detection is critical
- Use **Hybrid IDS** when coverage and accuracy are both priorities

---

## 🔎 Task 3 - IDS Example: Snort

![Snort Modes Illustration](https://github.com/user-attachments/assets/82d40e53-4c85-4a85-9951-f0e9d17ebae5)

**Snort** is one of the most popular open-source IDS tools. Developed in 1998, it supports:

- Real-time traffic analysis
- Protocol analysis
- Content matching
- Packet logging

### 🧪 Snort Modes

| Mode | Purpose | Usage Example |
|------|---------|----------------|
| **Packet Sniffer** | Just view packets | Diagnose performance issues |
| **Packet Logger** | Save packets as logs (PCAP) | Forensic analysis |
| **NIDS Mode** | Analyze traffic & trigger alerts | Detect known intrusions in real-time |

Snort relies heavily on **rules** to determine what traffic is suspicious.

---

## ⚙️ Task 4 - Snort Usage


![Snort Rule Syntax Breakdown](https://github.com/user-attachments/assets/cc334c4c-3fbd-461a-861a-329f7bf69759)

![Snort Engine - Packet Analysis](https://github.com/user-attachments/assets/3ed1a9f0-c01f-419b-a7fe-7baa0847124e)


### 🗂 File Structure

After installation, Snort's configuration and rules reside under:

```
/etc/snort/
```

Key files and folders:

- `snort.conf`: Main configuration
- `rules/`: Contains predefined and custom rule sets
- `local.rules`: Custom user rules

---

### 🧾 Snort Rule Syntax (Example)

```snort
alert icmp any any -> $HOME_NET any (msg:"Ping Detected"; sid:10001; rev:1;)
```

| Part | Meaning |
|------|---------|
| `alert` | Action (other options: log, drop, reject) |
| `icmp` | Protocol |
| `any any -> $HOME_NET any` | Source IP/port → Destination IP/port |
| `msg` | Message for alert |
| `sid` | Unique rule ID |
| `rev` | Revision number of the rule |

---

### ✍️ Creating a Custom Rule

1. Open local.rules:
```bash
sudo nano /etc/snort/rules/local.rules
```

2. Add custom rule:
```snort
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
```

3. Save and exit.

---

### 🚀 Run Snort in Detection Mode

To detect traffic matching your rules:

```bash
sudo snort -q -l /var/log/snort -i lo -A console -c /etc/snort/snort.conf
```

> Replace `lo` with your interface if different.

### 🔁 Test the Rule

```bash
ping 127.0.0.1
```

Expected output:
```
[**] [1:10003:1] Loopback Ping Detected [**] {ICMP} 127.0.0.1 -> 127.0.0.1
```

---

### 🧪 Analyze PCAP File

To inspect saved network traffic (forensics):

```bash
sudo snort -q -l /var/log/snort -r /etc/snort/Task.pcap -A console -c /etc/snort/snort.conf
```

> Use this for incident response or breach investigations.

---

## 🧪 Task 5 - Practical Lab

### 🧷 Scenario

You are a **forensic investigator**.  
Your client provides a PCAP file named `Intro_to_IDS.pcap` located in `/etc/snort/`.

Your task: **Analyze this file** using Snort and answer questions related to the intrusions inside.

### 🧪 Command to Use

```bash
cd /etc/snort
sudo snort -q -l /var/log/snort -r Intro_to_IDS.pcap -A console -c /etc/snort/snort.conf
```

---

## ✅ Conclusion

### 🔒 What You’ve Learned

- How IDS complements firewalls
- Difference between HIDS, NIDS
- How Snort operates in different modes
- Writing and testing custom detection rules
- How to investigate historical traffic with PCAP files

---

## 📘 Recommended Next Steps

- Learn Snort advanced rule writing
- Compare **IDS vs IPS** (Intrusion Prevention Systems)
- Try alternative tools like **Suricata** or **Zeek**
- Explore centralized logging with **SIEM integration**

---

## 💡 Pro Tip

An IDS without alert monitoring is like a silent alarm.  
Always integrate with real-time alerting or SIEM platforms for maximum effectiveness.
