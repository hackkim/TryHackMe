# 📡 Wireshark: The Basics - TryHackMe Room Summary

> A comprehensive walkthrough for the **Wireshark: The Basics** room on TryHackMe.  
> This guide is designed for beginners learning packet analysis and network investigation using Wireshark.

---

## 🧩 Task 1: Introduction

**Wireshark** is an open-source, cross-platform packet analysis tool used for:
- Capturing and analyzing live traffic.
- Investigating packet captures (PCAP files).
- Learning protocol structures and behaviors.

This TryHackMe room provides:
- A virtual machine (VM) in split-view mode (no SSH or RDP required).
- Two PCAP files:  
  - `http1.pcapng`: Used for demonstration and practice.  
  - `Exercise.pcapng`: Used to answer questions in the room.

---

## 🔍 Task 2: Tool Overview

### 🛠️ Use Cases
Wireshark is a versatile tool for:
- **Network troubleshooting** (e.g., packet loss, latency, congestion).
- **Security analysis** (e.g., detecting anomalies, identifying rogue hosts).
- **Protocol learning** (e.g., dissecting HTTP, TCP/IP behavior).

> Note: Wireshark is not an Intrusion Detection System (IDS). It does not alert you automatically—it’s up to the analyst to interpret packet behavior.

---

### 🖥️ Wireshark Interface Components

| Component | Description |
|----------|-------------|
| **Toolbar** | Access to menus for capture, filters, and analysis tools |
| **Display Filter Bar** | Field to enter display filters for analyzing packets |
| **Recent Files** | List of recently opened PCAPs |
| **Capture Filters and Interfaces** | Options to select network interfaces and apply capture filters |
| **Status Bar** | Displays session info, active profile, and packet counts |

![Wireshark Interface Overview](https://github.com/user-attachments/assets/309fc7fd-848d-4ce7-bddd-9bcc0a0e11fa)

---

### 📂 Loading PCAP Files

PCAP files can be loaded by:
- Using `File → Open`
- Dragging and dropping the file into the window
- Double-clicking the file

Once opened, the window includes:
- **Packet List Pane** (summary of captured packets)
- **Packet Details Pane** (protocol-level breakdown)
- **Packet Bytes Pane** (hex + ASCII view of raw data)

![Packet Window Overview](https://github.com/user-attachments/assets/7f1de2a7-d7b5-403c-b890-c550f5d40f8f)

---

### 🎨 Packet Coloring

Color rules help visually distinguish protocols and anomalies.

- **Temporary rules**: Active for current session only.
- **Permanent rules**: Saved with profiles and reused automatically.

Configure via:
- `View → Coloring Rules`
- `View → Colorize Conversation`

![Coloring Rules](https://github.com/user-attachments/assets/75c26026-6093-4d28-ba88-e6861caa8664)

---

### 🦈 Capturing Traffic

Start and stop live packet capture using:
- ▶️ Blue shark icon: Start
- ⏹️ Red square: Stop
- 🔁 Green arrow: Restart

![Capture Interface](https://github.com/user-attachments/assets/0812b1ee-c076-4456-a4e4-28e4cf0c0b14)

---

### 🔗 Merging PCAP Files

Wireshark allows merging multiple PCAPs:
- Use `File → Merge`
- Save the merged capture for future analysis

![Merging PCAP Steps](https://github.com/user-attachments/assets/564eb153-e74e-4f58-a486-d0ac0fb1c24b)

---

### 🧾 Viewing File Properties

Access via `Statistics → Capture File Properties`.  
Displays:
- File path and size
- Timestamps
- Hashes (SHA1, MD5)
- Interfaces and capture settings

![Capture File Properties](https://github.com/user-attachments/assets/ddb3363c-2aca-4425-9d90-f4abf744dc12)

---

## 🧬 Task 3: Packet Dissection

Wireshark dissects each packet according to OSI model layers.

### 📸 Packet Dissection Walkthrough – Visual Summary

Below is a step-by-step visual of how a specific packet (Frame 27) is dissected in Wireshark:

![Step 1 - Packet Selection and Highlighted Bytes](https://github.com/user-attachments/assets/1cf27490-a57c-4201-8807-167bda4376ae)  
*Selecting a packet highlights its corresponding bytes and loads all protocol layers.*

---

### 🔍 Details Pane with Hex View

Each protocol layer section—Ethernet, IP, TCP, HTTP—is decoded and shown in a structured tree. Clicking any field highlights the respective bytes.

![Step 2 - Ethernet and Hex Mapping](https://github.com/user-attachments/assets/94ed3eca-ccd9-4fe9-8a7b-eb71b8b2c656)  
*The Ethernet section displays source and destination MAC addresses, along with the raw hex bytes.*

---

### 🧠 Full Protocol Stack Breakdown

Here's the full structured view of all layers captured in Frame 27:

```plaintext
Frame 27: 214 bytes on wire, 214 bytes captured
Ethernet II: Src = fe:ff:20:00:01:00, Dst = Xerox_00:00:00
IP: Src = 216.239.59.99, Dst = 145.254.160.237
TCP: Src Port = 80, Dst Port = 3371, Seq = 778787098, Ack = 918692089
HTTP/1.1 200 OK (text/html)
```

![Step 3 - Full Protocol Stack](https://github.com/user-attachments/assets/8f2d5cff-405b-4e2b-96e9-08ebddb7c041)





**OSI Layer Breakdown**:
- **Layer 1: Frame**  
  ![Frame Info](https://github.com/user-attachments/assets/d0a6cd9e-84fd-4789-9b6b-4ed49adb90da)
- **Layer 2: Ethernet**  
  ![Ethernet Info](https://github.com/user-attachments/assets/38cfcbe9-7127-4bac-9de1-70c100e379de)
- **Layer 3: IPv4**  
  ![IP Info](https://github.com/user-attachments/assets/7b2efef8-ffe6-47df-9a2b-3bddd775fd06)
- **Layer 4: TCP**  
  ![TCP Info](https://github.com/user-attachments/assets/23e82a56-591c-4af3-a4db-f9e6c2da9286)
- **Reassembled TCP Segment**  
  ![Reassembly](https://github.com/user-attachments/assets/52f5b3be-aed1-4580-930c-c002fcb4404a)
- **Layer 5: HTTP Protocol**  
  ![HTTP Response](https://github.com/user-attachments/assets/917e5077-3262-4d62-bc8c-d76c458b099f)
- **Application Data**  
  ![HTML Data](https://github.com/user-attachments/assets/a461c953-6568-457f-87a2-872165840f43)

---

## 🧭 Task 4: Packet Navigation

### Packet Numbering

Each packet has a unique number, visible on the leftmost column.

![Packet Numbering](https://github.com/user-attachments/assets/bd62ac0b-299e-4830-8a10-18d91029b5d2)

---

### Go to Packet

Quick navigation to a specific packet:
- `Go → Go to Packet` (`Ctrl + G`)
- Enter packet number and jump

![Go to Packet](https://github.com/user-attachments/assets/37ed6e67-7b54-4bc9-89ff-340dc8803f52)

---

### Find Packet

Search inside PCAP by:
- String
- Hex
- Regex
- Display filter

![Find Packet](https://github.com/user-attachments/assets/2e7896fa-0fb0-48c0-9d45-3ffa3231b665)

---

### Marking Packets

Highlight important packets for investigation using:
- `Ctrl + M`
- Right-click → Mark/Unmark

![Mark Packets](https://github.com/user-attachments/assets/6a4328a7-601f-42e9-afca-7c6bad50d898)

---

### Packet Comments

Add annotations to packets:
- `Edit → Packet Comment`
- Saved in the capture file

![Packet Comments](https://github.com/user-attachments/assets/45c3b4f9-ce92-4d50-b31c-aab9750fa9a9)

---

### Export Packets

Export only selected/marked/displayed packets:
- `File → Export Specified Packets`

![Export Packets](https://github.com/user-attachments/assets/e1088fa8-6810-43f4-87e1-b65eacf50cf8)

---

### Export Objects (e.g., HTTP files)

- Extract transferred files via `File → Export Objects → HTTP`

![Export Objects](https://github.com/user-attachments/assets/fc6c3a5c-f1d3-4613-b403-de3060ebb904)

---

### Time Display Format

Change time view for better analysis:
- `View → Time Display Format`

![Time Format Change](https://github.com/user-attachments/assets/78c6f7c2-871b-4f1b-a8a8-7eb188fce562)
![Time Format Comparison](https://github.com/user-attachments/assets/afed4ccd-373e-4f7a-8838-0ccf70dd4438)

---

### Expert Info

Displays errors, warnings, and protocol info:
- `Analyze → Expert Information`

![Expert Info](https://github.com/user-attachments/assets/cf8f8fc4-7d2c-4c4b-9dfe-92adde9a9f28)

---

## 🧪 Task 5: Packet Filtering

Wireshark supports two types of filters:
- **Capture Filter**: Filters traffic *before* capture
- **Display Filter**: Filters traffic *after* capture

---

### Apply as Filter

![Apply as Filter](https://github.com/user-attachments/assets/63bac19b-ffb6-4375-89b4-9dacc928677e)

---

### Conversation Filter

Filter based on IP + port flow:
- `Conversation Filter → TCP`

![Conversation Filter](https://github.com/user-attachments/assets/e0711bb5-a83a-4788-a2ea-8ba6878d5df4)

---

### Colourise Conversation

Highlights related packets without filtering them.

![Colorise Conversation](https://github.com/user-attachments/assets/c0054f6b-f5b4-4f4c-8d86-2fa4abf09ec7)

---

### Prepare as Filter

Create filter strings without applying them immediately.

![Prepare as Filter](https://github.com/user-attachments/assets/aaac3e1c-e05e-4eb7-8743-b15a2a76df23)

---

### Apply as Column

Add custom columns in packet list for selected fields.

![Apply as Column](https://github.com/user-attachments/assets/c2a44906-b91b-4b09-8724-a08e4670826b)

---

### Follow TCP Stream

Reconstructs the entire TCP session for application-level inspection.

![Follow TCP Stream](https://github.com/user-attachments/assets/c3679bf8-7081-483b-806e-58f213c01728)

---

## ✅ Task 6: Conclusion

You’ve completed **Wireshark: The Basics**!

You now understand:
- How to dissect packets layer by layer
- How to use filters to isolate key information
- How to mark, comment, extract and follow traffic
- How to interpret protocol behavior using Expert Info

👉 Next recommended room: **Wireshark: Packet Operations**

---

📘 _Created by: Kim Sunghoon_  
_For learning cybersecurity, red teaming, and network analysis using Wireshark_
