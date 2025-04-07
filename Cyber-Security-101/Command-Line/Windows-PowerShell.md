# ⚡ TryHackMe - Windows PowerShell

> Learn and unleash the power of Windows PowerShell through basic to advanced task automation, scripting, and system management.

---

## 🏴‍☠️ Task 1 - Introduction

![PowerShell Pirate Flag](https://github.com/user-attachments/assets/d3dcb3a2-90cd-48ba-a237-e8bbe982f723)

Welcome aboard, matey! This room will guide you through the fundamentals of PowerShell. Whether you're here out of curiosity or as a natural next step after the Windows Command Line room, prepare to explore the full potential of Microsoft's powerful shell environment.

### 🎯 Learning Objectives
- Understand what PowerShell is and what makes it powerful.
- Learn the basic structure of PowerShell’s language.
- Run essential PowerShell commands (cmdlets).
- See how PowerShell applies in cybersecurity and administration.

### 🧠 Prerequisites
Before starting, ensure you’ve completed:
- **Windows and AD Fundamentals**
- **Windows Command Line**

---

## 📘 Task 2 - What Is PowerShell

![PowerShell Hook and Laptop](https://github.com/user-attachments/assets/bb1e5216-4cab-44df-8b3d-03744753a26d)

PowerShell is a cross-platform task automation tool consisting of:
- A command-line shell
- A scripting language
- A configuration management framework

It’s built on the .NET framework and supports structured, object-oriented commands—making it vastly more powerful than `cmd.exe`. Originally Windows-only, PowerShell is now available on macOS and Linux, broadening its reach.

---

## 🖥️ Task 3 - PowerShell Basics

To begin, let’s connect to our target VM using **Remmina**. Here's how:

### 1. Open Remmina

![Open Remmina Menu](https://github.com/user-attachments/assets/1d66aede-7407-4e42-849b-3f67b787b115)

- Navigate to `Applications` → `Internet` → `Remmina`.

---

### 2. Bypass Keyring Prompt

![Keyring Popup](https://github.com/user-attachments/assets/bcc4bfca-a802-403a-8b65-71cefaea9b30)

- You may see a "login keyring" prompt.
- Click **Cancel** to proceed.

---

### 3. Configure SSH Connection

![Remmina SSH Select](https://github.com/user-attachments/assets/53a72901-44d4-40c0-b80e-57c57aa8d8a8)

- Select **SSH** from the dropdown.
- Enter the target IP in the field next to it.
- Press **Enter** to connect.

---

### 4. Enter SSH Credentials

![Credentials Card](https://github.com/user-attachments/assets/82779c8c-792f-4763-ba23-239fc430c5e6)

Use the credentials provided:
```
Username: captain
Password: JollyR0ger#
IP: MACHINE_IP
```

Once connected, launch PowerShell:
```cmd
powershell
```

You’ll see the PowerShell prompt:
```
PS C:\Users\captain>
```

---

## 🗂️ Task 4 - Navigating the File System and Working with Files

PowerShell uses `Get-ChildItem`, `Set-Location`, and other cmdlets to interact with files and directories—similar to `ls`, `cd`, `mkdir`, and `rm` in Unix-like shells.

```powershell
Get-ChildItem
Set-Location -Path ".\Documents"
New-Item -Path ".\test-folder" -ItemType "Directory"
Remove-Item -Path ".\test-folder"
```

---

## 🔍 Task 5 - Piping, Filtering, and Sorting Data

PowerShell pipelines **objects**, not just plain text. This allows for advanced chaining of commands:

```powershell
Get-ChildItem | Sort-Object Length
Get-ChildItem | Where-Object -Property Extension -eq ".txt"
```

You can also use:
- `Select-Object` for specific properties
- `Select-String` to search content inside files (similar to `grep`)

---

## 🧾 Task 6 - System and Network Information

Retrieve information about the machine and network:

```powershell
Get-ComputerInfo
Get-LocalUser
Get-NetIPConfiguration
Get-NetIPAddress
```

These commands are similar to `systeminfo` and `ipconfig` but return rich object data.

---

## 🔎 Task 7 - Real-Time System Analysis

Use the following cmdlets to monitor real-time activity:

```powershell
Get-Process           # Shows running processes
Get-Service           # Service status
Get-NetTCPConnection  # TCP connection status
Get-FileHash -Path .\example.txt  # Generate SHA256 hash
```

These are useful for system diagnostics, threat hunting, and incident response.

---

## ✍️ Task 8 - Scripting

PowerShell scripts automate everything from system configuration to penetration testing.

```powershell
Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Culture }
```

This command runs a remote script. With `Invoke-Command`, you can:
- Automate tasks on multiple machines
- Execute scripts in remote sessions
- Use variables and logic just like in full programming languages

---

## 🏁 Task 9 - Conclusion

🎉 Congratulations! You’ve explored:
- Core concepts and syntax of PowerShell
- How to use cmdlets, filter data, and retrieve system info
- Practical scripting and security applications

> Continue the journey in the [Linux Command Line](#) room!

Fair winds and sharp scripts, pirate!
