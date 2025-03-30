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
![fg command](https://github.com/user-attachments/assets/ca6e8082-ad22-4993-bbbd-f220520582b7)

### 🖼️ Image  
![script resumed](https://github.com/user-attachments/assets/8c8fcddd-f70f-456c-826e-8569cbdaf293)

---

## 🔁 Task 6: Automation with Crontabs

To edit crontab:
```bash
crontab -e
```

### 🖼️ Image  
![crontab editor](./스크린샷 2025-03-30 오후 12.00.38.png)

### 🖼️ Image  
![crontab generator](./스크린샷 2025-03-30 오후 12.00.06.png)

### 🖼️ Image  
![crontab entry](./스크린샷 2025-03-30 오후 12.00.11.png)

---

## 📦 Task 7: Package Management

### APT Directory
```bash
ls /etc/apt
```

### 🖼️ Image  
![APT Directory](./스크린샷 2025-03-30 오후 12.00.20.png)

### sources.list Contents
### 🖼️ Image  
![APT sources list](./스크린샷 2025-03-30 오후 12.00.26.png)

### Add a Community Repo
```bash
touch /etc/apt/sources.list.d/sublime-text.list
nano sublime-text.list
```

### 🖼️ Image  
![APT .list entry](./스크린샷 2025-03-30 오후 12.00.32.png)

### 🖼️ Image  
![Sublime APT entry](./스크린샷 2025-03-30 오후 12.00.38.png)

---

## 📄 Task 8: Logging & Monitoring

### 🖼️ Image  
![Log directories](./스크린샷 2025-03-30 오후 12.00.46.png)

### Apache Logs
### 🖼️ Image  
![Apache access/error logs](./스크린샷 2025-03-30 오후 12.00.52.png)

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
