# 🕵️ TryHackMe - Digital Forensics Intro (Detailed Markdown)

---

## 📘 Task 1 - Introduction to Digital Forensics


### 🖼️ Crime Scene & Case Evidence

#### 📍 Digital Crime Scene
![Crime Scene with Devices](https://github.com/user-attachments/assets/225c198c-c33b-4e42-b51c-dab87a57678b)

#### 🗺️ Bank Map Found on Device
![Bank Map Evidence](https://github.com/user-attachments/assets/80fe1aa8-63b4-46b3-be19-89d227a2b38a)


**Digital Forensics** is the use of forensic science to investigate cyber crimes involving digital devices. It helps law enforcement agencies retrieve, analyze, and preserve digital evidence in a legal manner.

### 🧠 Key Highlights:
- Digital crime is rising due to widespread use of digital devices.
- Every digital interaction leaves behind traces (artifacts).

### 🧾 Example Case:
A bank robber’s home was raided. Devices like laptops, hard drives, and phones were seized. Forensics uncovered:
- Bank blueprints on the laptop
- Security bypass plans on a hard drive
- Photos/videos of prior crimes
- Illegal chats and call records on the phone

### 🎯 Learning Objectives:
- Understand phases of digital forensics
- Differentiate forensic types
- Learn evidence acquisition best practices
- Explore Windows forensics
- Practice through a hands-on investigation

---

## 🔍 Task 2 - Digital Forensics Methodology


### 🖼️ Digital Forensics Process & Scope

#### 📊 NIST Forensics Lifecycle
![Forensics Phases](https://github.com/user-attachments/assets/de3b4f95-1aa5-489a-bfcd-bba98db731ef)

#### 🌐 Digital Forensics Categories
![Forensics Categories](https://github.com/user-attachments/assets/d5eee94b-e033-4c4c-bced-fc922c8b998f)


Defined by **NIST**, the digital forensics lifecycle has 4 phases:

### 🧪 1. Collection
- Identify sources (PCs, USBs, mobile, etc.)
- Ensure original data is intact (no alteration)
- Maintain detailed logging (timestamps, evidence tags)

### 📂 2. Examination
- Filter large datasets
- Narrow scope (e.g., by user, date, file type)
- Extract case-relevant data

### 🔬 3. Analysis
- Correlate artifacts chronologically
- Reconstruct suspect activity
- Use timelines, hashes, keyword searches

### 🧾 4. Reporting
- Prepare technical + executive-level summaries
- Include methods, findings, recommendations

---

### 🔄 Types of Digital Forensics:

| Type | Description |
|------|-------------|
| Computer Forensics | Investigates PCs and laptops |
| Mobile Forensics | Extracts SMS, call logs, GPS from mobile devices |
| Network Forensics | Analyzes logs and packet captures |
| Database Forensics | Investigates unauthorized data access or tampering |
| Cloud Forensics | Focuses on off-site cloud-stored data |
| Email Forensics | Reviews email headers, content, phishing trails |

---

## 🧷 Task 3 - Evidence Acquisition


### 🖼️ Evidence Acquisition Procedures

#### 📜 Legal Search Authorization
![Search Warrant](https://github.com/user-attachments/assets/44216091-5bac-44bf-9d7b-1152af16df4a)

#### 🔌 Write Blocker Device in Action
![Write Blocker and Hard Drive](https://github.com/user-attachments/assets/f8b7d7ce-8438-4233-ac47-faaf9538b42b)



### ✅ Guidelines:

- **Authorization**: Always obtain legal permission before acquiring evidence.
- **Chain of Custody**: Maintain documentation for every step:
  - Evidence ID, type, owner, access history
  - Storage location

```plaintext
Chain of Custody Record:
  ID: USB-002
  Collected by: J. Smith @ 2024-04-12 14:32
  Location: Evidence Locker #3
```

- **Write Blockers**: Prevent modification of source storage (especially HDDs/SSDs)

> Using write blockers ensures evidence integrity.

---

## 🪟 Task 4 - Windows Forensics


### 🖼️ Windows Forensics Tool Overview

#### 💽 FTK Imager (Disk Acquisition)
![FTK Disk Tool Icon](https://github.com/user-attachments/assets/564a9710-7d7b-492d-acb6-e16e4537735d)

#### 🐶 Autopsy Tool Symbol
![Autopsy Mascot](https://github.com/user-attachments/assets/ca131cff-87c1-476c-9043-79cfee57d2bd)

#### 📈 Volatility for Memory Analysis
![Volatility Icon](https://github.com/user-attachments/assets/fc138779-5942-48e8-ab76-04e6e2c16d5a)


### 🖥️ Evidence Types:
- **Disk Image** (non-volatile): Files, metadata, browsing history
- **Memory Image** (volatile): Open processes, network connections, command history

### 🧰 Key Tools:

| Tool | Purpose |
|------|---------|
| FTK Imager | Create/view disk images |
| Autopsy | Analyze disk images, recover files, keyword search |
| DumpIt | Command-line tool for RAM imaging |
| Volatility | Plugin-based memory image analysis (Windows/Linux/macOS) |

> Capture memory image **before shutdown** to preserve volatile evidence.

---

## 🔎 Task 5 - Practical Case: PDF & Image Metadata

### 🐾 Scenario:
A cat named *Gado* is kidnapped. You received a suspicious Word document, later converted to PDF. You’ll analyze the PDF and a photo it contains.

### 📄 Step 1: Analyze PDF Metadata
Tool: `pdfinfo`
```bash
pdfinfo DOCUMENT.pdf
```
Expected Output:
```plaintext
Creator: Microsoft Word for Office 365
CreationDate: Wed Oct 10 21:47:53 2018 EEST
Pages: 20
Encrypted: no
```

### 🖼️ Step 2: Extract EXIF Metadata from Image
Tool: `exiftool`
```bash
exiftool IMAGE.jpg
```
Sample Output:
```plaintext
Camera Model: iPhone 11 Pro
GPS Position: 51 deg 31' 4.00" N, 0 deg 5' 48.30" W
```

### 📍 Step 3: Locate GPS Coordinates
Convert GPS → Google Maps friendly:
```
51°31'04.0"N 0°05'48.3"W
```
Paste into [Google Maps](https://maps.google.com) → You’ve got the location!

---

## 🧠 Summary

- Digital forensics follows a structured method: **Collect → Examine → Analyze → Report**
- Multiple domains exist: PCs, mobile, cloud, networks
- Tools like `Autopsy`, `Volatility`, and `pdfinfo` aid in real-world investigations
- Metadata is a powerful source of hidden evidence

🧭 Stay curious. Every byte tells a story.
