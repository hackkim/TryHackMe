# 🐧 Linux Fundamentals Part 3 - TryHackMe Room Summary

Welcome to the final part of the Linux Fundamentals module! In this room, you'll explore practical utilities, automation, process management, and more to level up your Linux skills.

---

## 🧠 Task 1: Introduction

This room covers:
- Useful utilities and day-to-day Linux applications
- Automation with crontabs
- Package management using apt
- Logging and monitoring services

### 🖼️ Image  
![Linux Fundamentals Title](https://github.com/user-attachments/assets/38170091-2f3b-40d1-9c14-7dd933212cc5)

---

## 🚀 Task 2: Deploy Your Linux Machine

Deploy your **Linux Target Machine** and **AttackBox** to interact with remotely.

Use the following credentials:
- **Username**: tryhackme  
- **Password**: tryhackme

### 🖼️ Image  
![Target Machine Info](https://github.com/user-attachments/assets/e5b1e4b5-6cff-4551-9630-4cca1167afaa)

### 🖼️ Image  
![Start AttackBox](https://github.com/user-attachments/assets/0b7f9f22-db55-41a7-8fd1-adb7b3059db6)

---

## ✍️ Task 3: Terminal Text Editors

### 🧷 Nano
To edit a file:
```bash
nano myfile
```

Use:
- `^O` to save
- `^X` to exit

### 🧷 VIM
More advanced and powerful — supports customization, syntax highlighting, and wide compatibility.

### 🖼️ Image  
![VIM Screenshot](https://github.com/user-attachments/assets/1cbd26b0-d4aa-4024-b6f2-8f94e814165a)

---

## ⚙️ Task 4: General/Useful Utilities

### 📥 Downloading Files with wget
```bash
wget http://MACHINE_IP:8000/file.txt
```

### 🌐 Python3 Web Server
```bash
python3 -m http.server
```

### 🖼️ Image  
![wget Example](https://github.com/user-attachments/assets/2aed11f9-97dc-4939-b93b-71f574eda51d)

---

## 🧠 Task 5: Processes 101

### 🖼️ Image  
![ps output](https://github.com/user-attachments/assets/50a986d2-1456-47a4-8943-f850325252cf)

### 🖼️ Image  
![ps aux output](https://github.com/user-attachments/assets/561d9055-9b74-452e-ad0b-e1638e9b6f01)

### 🖼️ Image  
![top output](https://github.com/user-attachments/assets/6e16f31c-1ea8-4cc6-931d-26bd693789e2)

### 🖼️ Image  
![systemd PID 1](https://github.com/user-attachments/assets/55f4c7bb-6d56-440f-ac5a-c871c93dfd3b)

### Backgrounding with Ctrl+Z

### 🖼️ Image  
![Ctrl+Z Background](https://github.com/user-attachments/assets/136a91dd-6bea-4ba3-93d9-3b7c2b845825)

### 🖼️ Image  
![backgrounded ps aux](https://github.com/user-attachments/assets/a16a95a6-211e-4cfc-92b2-6d0e6e44f5a4)

### Foregrounding with fg
```bash
fg
```

### 🖼️ Image  
![fg command](https://github.com/user-attachments/assets/8c8fcddd-f70f-456c-826e-8569cbdaf293)

### 🖼️ Image  
![script resumed](https://github.com/user-attachments/assets/ca6e8082-ad22-4993-bbbd-f220520582b7)

---
## 🔁 Task 6: Maintaining Your System: Automation

Users may want to schedule certain tasks after the system boots — like running backup scripts or launching apps automatically.

We're going to focus on the **cron** process, specifically how to manage it with **crontab**. Crontab files are executed line by line based on time specifications.

### 🖼️ Image  
![crontab nano opened](https://github.com/user-attachments/assets/c873ced6-d7aa-46f0-a430-fa1542d2c2d8)

---

### 🧩 Crontab Format

A crontab entry follows this structure:

| Value | Description |
|-------|-------------|
| MIN   | Minute to execute at |
| HOUR  | Hour to execute at |
| DOM   | Day of the month |
| MON   | Month of the year |
| DOW   | Day of the week |
| CMD   | Command to run |

---

### 📁 Example

To backup a directory every 12 hours:

```cron
0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/
```

You can use asterisks `*` as wildcards.

Helpful tools:
- [Crontab Generator](https://crontab-generator.org)
- [Cron Guru](https://crontab.guru)

---

### 🖼️ Image  
![Cronjob result preview](https://github.com/user-attachments/assets/32514378-01a0-4ff3-84e1-19de807b889d)

---

You can edit your crontab with:

```bash
crontab -e
```

### 🖼️ Image  
![Crontab with backup line](https://github.com/user-attachments/assets/8464a8df-48a7-4210-a679-df36457b1e7a)

---

## 📦 Task 7: Package Management

### APT Directory
```bash
ls /etc/apt
```

### 🖼️ Image  
![APT Directory](https://github.com/user-attachments/assets/966eab83-cc22-418a-93a3-82ed8a108a34)

### sources.list Contents
### 🖼️ Image  
![APT sources list](https://github.com/user-attachments/assets/f04a9493-feeb-4464-a465-c3f9019cda9b)

### Add a Community Repo
```bash
touch /etc/apt/sources.list.d/sublime-text.list
nano sublime-text.list
```

### 🖼️ Image  
![APT .list entry](https://github.com/user-attachments/assets/079dbbf3-4f7d-4015-aacd-a95904f4cc8b)

### 🖼️ Image  
![Sublime APT entry](https://github.com/user-attachments/assets/02e46c06-2482-4f08-993a-ad62c52f47c2)

---

## 📄 Task 8: Logging & Monitoring

### 🖼️ Image  
![Log directories](https://github.com/user-attachments/assets/83032427-e8ef-4874-9aa4-8535826260b6)

### Apache Logs
### 🖼️ Image  
![Apache access/error logs](https://github.com/user-attachments/assets/deb0d1a6-e89d-4a0a-840f-f1c2f96984e2)

---

## ✅ Task 9: Conclusions & Summaries

Well done! Here's what you've accomplished:
- Used terminal editors like **nano** and **vim**
- Downloaded and served files
- Managed and monitored processes
- Automated tasks using **cron**
- Installed and removed software via **apt**
- Reviewed system and service logs

🔗 Continue your Linux journey:
- [Bash Scripting Room](https://tryhackme.com/room/bashscripting)
- [Regular Expressions Room](https://tryhackme.com/room/catregex)
