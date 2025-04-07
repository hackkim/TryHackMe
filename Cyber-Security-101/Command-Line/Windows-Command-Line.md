# 💻 TryHackMe - Windows Command Line

> Learn the essential Windows commands through practical exercises in the Windows Command Prompt environment.

---

## 🧭 Task 1 - Introduction

![Windows Command Line Icon](https://github.com/user-attachments/assets/06501a30-3393-4c40-949b-3d73fcb57b0c)
![SSH Connection Terminal](https://github.com/user-attachments/assets/2c5e6608-0809-44b5-9c96-2c04f91f2321)

A Command Line Interface (CLI) may seem daunting at first, especially when you're used to a Graphical User Interface (GUI). However, mastering the CLI will significantly improve your efficiency.

### 📌 Benefits of CLI
- **Lower Resource Usage**: Uses fewer resources than GUIs.
- **Automation**: Easily script repetitive tasks.
- **Remote Management**: Use SSH to manage servers or IoT devices efficiently.

### 🛠️ Learning Objectives
Learn how to:
- Display basic system information
- Check and troubleshoot network configuration
- Manage files and folders
- Check running processes

### 🚀 Start Machine Instructions
Use the TryHackMe AttackBox or your own terminal and connect via SSH:

```bash
ssh user@MACHINE_IP
# Password: Tryhackme123!
```

Follow the prompts to establish a secure SSH session.

---

## 📊 Task 2 - Basic System Information

![System Smile Monitor](https://github.com/user-attachments/assets/4e1ff5d9-9079-4c7e-bdbb-f250e2190b1f)

To start exploring your system configuration, try the following commands:

### 🔧 Useful Commands

```bash
set
ver
systeminfo
driverquery | more
```

### 📌 Notes:
- `set`: Shows environment variables and paths.
- `ver`: Displays OS version.
- `systeminfo`: Outputs detailed system specs.
- `driverquery | more`: Lists drivers page-by-page.
- `help`, `cls`: Get help or clear screen.

---

## 🌐 Task 3 - Network Troubleshooting

Explore network interfaces and connectivity using these commands:

### 🧾 IP Configuration
```bash
ipconfig
ipconfig /all
```

### 📡 Network Testing
```bash
ping example.com
tracert example.com
```

### 🌐 DNS Resolution
```bash
nslookup example.com
nslookup example.com 1.1.1.1
```

### 🔍 Network Statistics
```bash
netstat
netstat -abon
```

---

## 📂 Task 4 - File and Disk Management

### 📁 Directory Navigation
```bash
cd
cd ..
dir
tree
```

### 📦 Create/Delete Directories
```bash
mkdir <dir_name>
rmdir <dir_name>
```

### 📄 View and Manage Files
```bash
type file.txt
more file.txt
copy file1.txt file2.txt
move file.txt ..
del file2.txt
```

### ⭐ Wildcard Example
```bash
copy *.md C:\Markdown
```

---

## 🧾 Task 5 - Task and Process Management

Manage processes directly from the command line.

### 👀 View All Tasks
```bash
tasklist
```

### 🔍 Filter Specific Tasks
```bash
tasklist /FI "imagename eq sshd.exe"
```

### 💣 Kill a Task
```bash
taskkill /PID 2712
taskkill /PID 2712 /F  # Force kill
```

### ❔ Get Help
```bash
tasklist /?
taskkill /?
```

---

## ✅ Task 6 - Conclusion

We have now covered essential Windows command line tools:

### 🛠️ Categories Covered
- **System**: `ver`, `systeminfo`, `driverquery`
- **Network**: `ipconfig`, `ping`, `tracert`, `netstat`
- **Files**: `cd`, `dir`, `mkdir`, `copy`, `move`, `del`
- **Processes**: `tasklist`, `taskkill`

### 📚 Additional Useful Commands
```bash
chkdsk
sfc /scannow
```

💡 **Tips**:
- Use `/h` or `/?` with most commands to view help.
- Use `| more` to scroll long output.

---

➡️ Ready for the next level? Head to the [Windows PowerShell](#) room.
