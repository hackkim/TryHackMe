# 🪟 TryHackMe - Windows Fundamentals 2

> Continuing the journey exploring the Windows operating system tools and configuration utilities.

---


## 🧭 Task 1 - Introduction

We will continue our journey exploring the Windows operating system.  
In Windows Fundamentals 1, we covered the desktop, the file system, user account control, the control panel, settings, and the task manager.

This module will provide an overview of additional utilities and ways to access them.

**VM Credentials**
- IP: `MACHINE_IP`
- User: `administrator`
- Password: `letmein123!`

📌 VM Start Interface  
![VM Interface](https://github.com/user-attachments/assets/6e025b69-71a5-4b7f-9905-e96257cb6c5e)

📌 RDP Login Example  
![RDP Login](https://github.com/user-attachments/assets/a9fa4033-3548-44b1-bb55-b4abc2af6381)

> Accept the Certificate when prompted. The VM may take up to 3 minutes to fully boot.

---

## 📋 Task Summary

Here’s a brief summary of what each task in this room covers:

| Task | Topic                        | Summary                                                                 |
|------|------------------------------|-------------------------------------------------------------------------|
| 1    | Introduction                 | Overview of the room's goals and VM setup for exploring Windows tools. |
| 2    | System Configuration         | Use of MSConfig to troubleshoot startup, services, boot options, etc.  |
| 3    | Change UAC Settings          | How to change User Account Control levels using a slider UI.           |
| 4    | Computer Management          | Covers Task Scheduler, Event Viewer, Shared Folders, Device Manager, etc. |
| 5    | System Information           | Using `msinfo32` to inspect system specs, environment, and components. |
| 6    | Resource Monitor             | Viewing real-time usage of CPU, Disk, Memory, and Network.             |
| 7    | Command Prompt               | Basic commands like `hostname`, `ipconfig`, `net`, and their help menus. |
| 8    | Registry Editor             | Exploring and editing the Windows Registry (regedit).                  |
| 9    | Conclusion                   | Final notes and reminder that most tools are accessible outside MSConfig. |


---


## ⚙️ Task 2 - System Configuration (msconfig)

System Configuration (`msconfig`) is used to manage startup behavior, services, boot settings, and access system tools.

---

📌 Launching MSConfig via Start Menu:  
![Launch MSConfig](https://github.com/user-attachments/assets/3c5df7ad-0a70-4b12-9cd5-9692116e1263)

---

### 🧩 MSConfig Tabs Overview

1. **General Tab**  
Configure how Windows should start: Normal, Diagnostic, or Selective.  
![MSConfig General Tab](https://github.com/user-attachments/assets/ac33aad6-c2c3-47f1-9d41-de253c46361b)

2. **Boot Tab**  
Define boot options such as Safe Boot, Boot log, etc.  
![MSConfig Boot Tab](https://github.com/user-attachments/assets/618b48e2-86f2-442a-9115-d12252144648)

3. **Services Tab**  
See all system services and enable/disable them.  
![MSConfig Services Tab](https://github.com/user-attachments/assets/89d2a052-1805-4371-b3d1-ede58dc392ab)

4. **Startup Tab**  
Redirects to Task Manager for startup program control.  
![MSConfig Startup Tab](https://github.com/user-attachments/assets/881a6c3d-109e-44b7-806d-dcd562b6ba89)

5. **Tools Tab**  
List of diagnostic tools with commands to launch them.  
![MSConfig Tools Tab](https://github.com/user-attachments/assets/7eb53dd3-1750-4ba8-83ac-7dfb3993a4c4)

---

> 🧠 What I Learned (Task 2)  
> - I didn’t know about the "Tools" tab before. It’s super useful!  
> - MSConfig is a great place to disable non-essential startup services safely.


---


## 🛡️ Task 3 - Change UAC Settings

User Account Control (UAC) settings help control how often you’re notified when apps make changes to your computer.

You can use a slider to configure UAC behavior:

- Always notify for high security
- Notify only when apps try to make changes
- Don’t notify (not recommended)

📌 UAC Settings Panel  
![UAC Settings](https://github.com/user-attachments/assets/1ada2b43-503b-491e-8ba8-702918b9f54f)

---

### 🧠 What I Learned (Task 3)
- UAC adds a layer of protection against unauthorized changes.
- I tested the slider and saw how different levels affect app prompts.

---

## 🖥️ Task 4 - Computer Management

Computer Management includes various tools grouped under System Tools, Storage, and Services.

📌 Main Computer Management View  
![Computer Management](https://github.com/user-attachments/assets/12fe5cf0-2433-4f97-bd81-e3b0289746f5)

---

### 🔧 Task Scheduler  
Allows automation of tasks on login, logoff, or scheduled intervals.  
![Task Scheduler](https://github.com/user-attachments/assets/d69d62a6-8778-4331-acd8-3e3011fb8d38)

---

### 📋 Event Viewer  
Audit trail for events such as system errors, logins, or warnings.  
![Event Viewer](https://github.com/user-attachments/assets/73ead0eb-754e-4f75-83c7-01ba39376cf4)  
📌 Event Types  
![Event Types](https://github.com/user-attachments/assets/846805e6-43ef-4ef2-a3b0-04fa0509add9)  
📌 Standard Logs  
![Windows Logs Table](https://github.com/user-attachments/assets/82d2e667-9498-4818-aa6a-7b12af9ca94e)

---

### 📂 Shared Folders  
View shared folders and connected users.  
![Shared Folders](https://github.com/user-attachments/assets/6f0188de-0ce3-42ed-889c-105941f7128e)

---

### 📈 Performance Monitor  
Real-time system performance metrics.  
![Performance Monitor](https://github.com/user-attachments/assets/4f1f24d1-abf4-4470-b09f-a023dada3b63)

---

### 🖱️ Device Manager  
Hardware configuration and troubleshooting.  
![Device Manager](https://github.com/user-attachments/assets/0cce91d4-af0d-45ec-83c0-41391e0f079f)

---

### 💾 Disk Management  
View and manage partitions and drives.  
![Disk Management](https://github.com/user-attachments/assets/5cdec33a-55ff-40a2-a966-389bdfa8bc1a)

---

### ⚙️ Services and Applications  
Manage background services and WMI configuration.  
![Services Panel](https://github.com/user-attachments/assets/41512e39-bb7e-4f79-8a0b-9682e84a45a3)

📌 Example: VMware SVGA Helper Service  
![Service Properties](https://github.com/user-attachments/assets/5e94b86d-b18d-43c9-9440-4f1fd49a3437)

---

### 🧠 What I Learned (Task 4)
- I didn’t realize how much is packed into Computer Management.
- Event Viewer logs are like a system journal — great for troubleshooting!

---

## 🖥️ Task 5 - System Information

Use `msinfo32` to get detailed system diagnostics and specs.

---

### 🧾 System Summary  
![System Summary](https://github.com/user-attachments/assets/ea97b60f-60c9-46b2-a1d9-56582dfc936f)

---

### 🔧 Hardware Resources  
![Hardware Resources](https://github.com/user-attachments/assets/e39bbd64-d8f0-4413-86ff-298303ac4f52)

---

### 🧱 Components  
![Components](https://github.com/user-attachments/assets/5d5bbac7-4e8b-4a9b-b1cd-093d309cd642)

---

### 🧩 Software Environment  
![Software Environment](https://github.com/user-attachments/assets/7c6731d8-b379-45bc-b964-c3bb84cea91b)

---

### 🌐 Environment Variables  
- View environment variables from within `msinfo32`  
![Environment Variables](https://github.com/user-attachments/assets/8d44d6e5-cf82-4d1d-80ae-a0d5391a11d1)

- Advanced system settings  
![Advanced Settings](https://github.com/user-attachments/assets/77fbcd0d-91c8-4131-9555-d6c99bbff92b)

---

### 🔍 Search IP Address  
![Search IP Address](https://github.com/user-attachments/assets/26561483-0129-49f5-a659-92e7dc4b6be4)

---

### 🧠 What I Learned (Task 5)
- `msinfo32` shows hardware, drivers, and OS version — all in one place.
- The built-in search is super helpful.

---

## 📊 Task 6 - Resource Monitor

Resource Monitor (`resmon`) provides detailed real-time monitoring for:

- CPU
- Disk
- Network
- Memory

---

### 🧩 Overview Tab  
![Overview Tab](https://github.com/user-attachments/assets/32a52afa-31d2-420d-b88f-3f68c5bee6d7)

---

### 🧭 Tabs  
![Tabs](https://github.com/user-attachments/assets/a59920ed-0e60-4731-9323-2010d0acf64b)

---

### 🔍 CPU  
![CPU Tab](https://github.com/user-attachments/assets/3b8495a9-1189-4397-972e-c5c7308d0563)

---

### 🧠 Memory  
![Memory Tab](https://github.com/user-attachments/assets/40d1729e-5217-46a7-bb2b-f79702cee34c)

---

### 💾 Disk  
![Disk Tab](https://github.com/user-attachments/assets/d6a41a9b-cbc2-4f27-a393-942f68b2c9a8)

---

### 🌐 Network  
![Network Tab](https://github.com/user-attachments/assets/36f56532-94f4-48b9-a0dd-dadb7557eb88)

---

### 🧠 What I Learned (Task 6)
- It gives way more insight than Task Manager.
- The real-time graphs helped me track down high disk usage.

---

## 💻 Task 7 - Command Prompt

Command Prompt allows users to perform tasks via CLI.

---

### 🖥️ Basic Commands

#### `hostname`  
![CMD hostname](https://github.com/user-attachments/assets/0e015c43-27af-4627-8dc9-44db4adc2ae5)

#### `whoami`  
![CMD whoami](https://github.com/user-attachments/assets/36c97288-b46b-4542-ba58-618f3cd5774b)

---

### 🌐 Network Commands

#### `ipconfig`  
![CMD ipconfig](https://github.com/user-attachments/assets/fad3847a-4ebc-481e-afe6-fcc47bb8ec7a)

#### `ipconfig /?`  
![CMD ipconfig help](https://github.com/user-attachments/assets/bbfac9ae-072d-4e1d-90ad-520c1edda335)

#### `netstat`  
![CMD netstat](https://github.com/user-attachments/assets/bb52fe52-0fcf-4339-b434-999c24bb6c62)

---

### 🧰 Net Commands

#### `net`  
![CMD net](https://github.com/user-attachments/assets/c3eb9eeb-3907-4e28-96a4-76c24f4cd02e)

#### `net help`  
![CMD net help](https://github.com/user-attachments/assets/6c7583e1-001f-498d-a2dd-b009f9db2211)

#### `net help user`  
![CMD net help user](https://github.com/user-attachments/assets/acbdf10b-2600-4014-ae46-4464273bc58a)

---

### 🧠 What I Learned (Task 7)
- `netstat` and `ipconfig` are handy for quick troubleshooting.
- `net help` shows a lot of command power I hadn’t used before.



## 🧬 Task 8 - Registry Editor

### 🧠 What I Learned (Task 8)
- The registry holds deep system configuration—it's powerful but risky.
- I found where startup programs are stored: `HKEY_LOCAL_MACHINE\...\Run`

The Windows Registry is a core part of the OS where configuration data is stored.

📌 Registry Editor (run via `regedit`)  
![Registry Editor](https://github.com/user-attachments/assets/c73843b1-d9b5-42d7-a895-ec727ef30c22)



## ✅ Task 9 - Conclusion

### 🧠 What I Learned (Task 9)
- Many tools can be opened from the Start Menu or Run (e.g. `eventvwr`, `perfmon`, `msinfo32`)
- Now I prefer `Win + R` instead of always searching manually.

You don’t always need MSConfig to open powerful tools. Most are accessible from:

- Start Menu
- Run Dialog (`Win + R`)
- CMD

📌 Example: Administrative Tools in Start Menu  
![Start Menu Tools](https://github.com/user-attachments/assets/813b6437-01d7-4d6f-8ca3-d2a65106d59d)
