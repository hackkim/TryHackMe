# 🛡️ TryHackMe - Windows Fundamentals 3

> A continuation of the Windows Fundamentals series, focusing on built-in **security features** of Windows.

---


## 🧭 Task 1 - Introduction

We continue our journey with Windows Fundamentals.

### ✅ Previously covered:
- **Fundamentals 1:** Desktop, file system, UAC, control panel, settings, task manager  
- **Fundamentals 2:** MSConfig, Computer Management, Resource Monitor, etc.  
- **Fundamentals 3:** Windows Security tools (Defender, Firewall, BitLocker, etc.)

This room focuses on the **security tools** and **protections built into Windows**.

**VM Login:**
- IP: `MACHINE_IP`
- Username: `administrator`
- Password: `letmein123!`

📌 Conceptual Overview  
![Windows Security Concept](https://github.com/user-attachments/assets/aa960c66-05fe-43ea-88d4-e040dcd165fd)

📌 RDP Login Settings  
![RDP Login Settings](https://github.com/user-attachments/assets/da6c6b4f-1d62-4039-b12a-f222fa74b5b4)

> Accept the Certificate when prompted. The VM may take up to 3 minutes to fully boot.


---


## 🔄 Task 2 - Windows Updates

Windows Update is a Microsoft service that provides patches, security updates, and feature enhancements.

---

### 🧭 Access Windows Update

📌 Navigate to: **Settings > Update & Security**  
![Windows Update Settings](https://github.com/user-attachments/assets/4598b3f5-2279-42a1-87ad-3eac4be90bb3)

---

### ⚙️ VM-Specific Update Info

- This VM's update settings are **managed by an organization**.
- **No updates available** (because it has no internet access).

📌 Managed / No Updates  
![Windows Update Status](https://github.com/user-attachments/assets/ac93ce1b-56a5-42db-9fb3-a807abeac66d)

---

### 🔁 Restart Required Example

When updates are pending, users are prompted to restart or schedule one.

📌 Restart Required  
![Restart Required Prompt](https://github.com/user-attachments/assets/8a199cfe-163b-4ebf-aa1f-11ff0fed1eea)

> ℹ️ Updates cannot be indefinitely postponed in Windows 10 and later.


---


## 🔐 Task 3 - Windows Security

Windows Security is the built-in hub for managing all of your device’s protection features.

It includes:
- Virus & threat protection
- Firewall & network protection
- App & browser control
- Device security

📌 Access from Settings  
![Windows Security Settings](https://github.com/user-attachments/assets/e8161da1-9e75-4a88-9d90-749f0f55798f)

---

📌 Security Overview (Real-Time Status)  
![Windows Security Glance](https://github.com/user-attachments/assets/b0186636-8dae-4f32-bc3b-94f919feeb23)

---

📌 Windows 10 Home/Pro Example View  
![Windows Security Win10](https://github.com/user-attachments/assets/e1634138-1269-4c52-b26b-023d9dcbfb69)

> ✅ Icons:
> - Green: Protected  
> - Yellow: Needs review  
> - Red: Needs immediate action


---


## 🦠 Task 4 - Virus & Threat Protection

This section covers real-time scanning, protection settings, threat history, and ransomware protection.

---

### 🔍 Current Threats
View last scan results and current threat status.  
![Current Threats](https://github.com/user-attachments/assets/2d5941d7-d35d-404d-95d4-2b8c2a27e4fa)

---

### ⚙️ Protection Settings and Updates
Manage real-time protection, cloud delivery, sample submission, and more.  
![Protection Settings](https://github.com/user-attachments/assets/3981f154-58a7-48cd-a287-76316645095b)

---

### 🖱️ On-Demand Scan (Right-Click)
Perform a scan on any file/folder from the context menu.  
![Right Click Defender](https://github.com/user-attachments/assets/e3214632-686a-451d-8024-30fb4137651e)

---

> 🧠 What I Learned (Task 4)
> - Real-time protection should always be enabled unless replaced by another trusted AV.
> - Right-click scanning is a quick way to check downloaded files.


---


## 🔥 Task 5 - Firewall & Network Protection

The firewall controls what traffic is allowed in and out of your device.

---

### 🌐 Network Profiles  
Shows current status for Domain, Private, and Public networks.  
![Firewall Overview](https://github.com/user-attachments/assets/b7ba3716-a719-4a9a-b4d5-237eef4d6b48)

---

### 🛡️ Private Profile  
Firewall state and option to block all incoming connections.  
![Private Profile](https://github.com/user-attachments/assets/1acac836-9010-4759-8da3-2f42446a8384)

---

### ✅ Allowed Apps  
Customize app access to firewall under private/public profiles.  
![Allowed Apps](https://github.com/user-attachments/assets/704bfa95-ee18-46c7-8fc9-8dc7883e7674)

---

### ⚙️ Advanced Firewall Settings  
Rule-based control over inbound and outbound traffic.  
![Advanced Firewall](https://github.com/user-attachments/assets/cae316bb-5a21-4df1-a280-27afd319a95b)

---

> 🧠 What I Learned (Task 5)
> - I now understand the difference between Domain, Private, and Public profiles.
> - The advanced settings look intimidating but offer powerful control.

---


## 🌐 Task 6 - App & Browser Control

This section allows you to manage settings for Microsoft Defender SmartScreen and Exploit Protection.

---

### 🛡️ SmartScreen Configuration

📌 SmartScreen UI  
![App and Browser Control](https://github.com/user-attachments/assets/a2fbc04c-54d5-45ab-8e15-5b3e59ac2a6b)

📌 Blocked App Warning  
![SmartScreen Warning](https://github.com/user-attachments/assets/8d80d2af-9e42-4d3b-8cdc-b7f7816ad61f)

---

### 🔒 Exploit Protection

Windows includes built-in mitigation against memory and execution-based attacks.

📌 Exploit Protection Settings  
![Exploit Protection Settings](https://github.com/user-attachments/assets/a5cefd12-dca8-447d-b02f-0f5fe44b0f55)

---

> 🧠 What I Learned (Task 6)
> - SmartScreen adds a layer of defense for unknown apps.
> - Exploit Protection is built-in and can be fine-tuned if needed.


---


## 💻 Task 7 - Device Security

This section provides insight into virtualization-based protections and your device’s security processor (TPM).

---

### 🧰 Core Isolation

📌 Device Security Panel  
![Device Security](https://github.com/user-attachments/assets/242f9e2a-74a4-4874-aa81-6fe5cd562f65)

📌 Memory Integrity Setting  
![Memory Integrity](https://github.com/user-attachments/assets/f43f62ab-5fe3-4d35-9dcf-93806dc47389)

---

### 🔒 Security Processor (TPM)

📌 TPM Module Summary  
![Security Processor](https://github.com/user-attachments/assets/dfb7fa45-3fdd-4a73-b302-3eec12d8eb06)

📌 TPM Module Details  
![TPM Details](https://github.com/user-attachments/assets/6429925a-3362-4b31-b7f0-b45e2b5808ce)

---

> 🧠 What I Learned (Task 7)
> - Memory integrity helps defend against kernel-level exploits.
> - TPM enhances encryption and platform-level security.


---

## 🔐 Task 8 - BitLocker

BitLocker protects drives via encryption tied to hardware (TPM).

> 📝 Not available on the attached VM  
(ℹ️ No image required)

---


## 🗂️ Task 9 - Volume Shadow Copy Service (VSS)

Volume Shadow Copy Service (VSS) lets Windows take point-in-time snapshots of data for backup and restore purposes.

---

### 🔁 Accessing Shadow Copy Options

📌 Right-click a drive → "Configure Shadow Copies..."  
![Configure Shadow Copies](https://github.com/user-attachments/assets/ea4fb18a-a952-4559-87b1-fd6bf7eadeea)

---

### ⚙️ Shadow Copy UI

📌 Volume Configuration Window  
![Shadow Copy Settings](https://github.com/user-attachments/assets/2aa0c223-c394-4931-9d64-596e7ff50555)

---

> 🧠 What I Learned (Task 9)
> - Shadow copies are powerful for recovery — if malware hasn’t wiped them!
> - Good backups must include off-site or offline storage as VSS copies can be deleted.


---

🔗 [Living Off The Land (LOLBAS)](https://lolbas-project.github.io/)


## ✅ Task 10 - Conclusion

Throughout this module, we explored the **built-in Windows security tools** available to protect your system:

- 🛡️ Windows Updates – patching vulnerabilities
- 🔐 Microsoft Defender Antivirus – real-time malware protection
- 🔥 Windows Firewall – managing network access
- 🧠 SmartScreen & Exploit Protection – preventing malicious behavior
- 💻 Device Security & TPM – hardware-based security support
- 📁 BitLocker (concept) – drive encryption using TPM
- 🗂️ Shadow Copies – recovery through restore points

> 🚨 Note: Many attackers use these same built-in tools to avoid detection (called Living Off The Land). Learn more about [LOLBins](https://lolbas-project.github.io/)

---

### 📚 Further Learning Resources

- [Antimalware Scan Interface (AMSI)](https://learn.microsoft.com/en-us/windows/win32/amsi/antimalware-scan-interface-portal)
- [Credential Guard Overview](https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/credential-guard)
- [Windows Hello](https://learn.microsoft.com/en-us/windows/security/identity-protection/hello-for-business/hello-identity-verification)
- [CSO Online: Best Windows 10 Security Features](https://www.csoonline.com/article/3251714/the-best-new-security-features-in-windows-10.html)
