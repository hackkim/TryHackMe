# 🖥️ TryHackMe - Windows Fundamentals 1

> A detailed walkthrough of Windows OS basics using the TryHackMe virtual environment  
> Author: [Your Name]  
> Source: [TryHackMe - Windows Fundamentals 1](https://tryhackme.com/room/windowsfundamentals1)

---

## 🧭 Task 1 - Introduction to Windows

- Windows OS is one of the most widely used operating systems in the world.
- It features a graphical user interface (GUI) and a wide variety of tools and settings.
- This module provides hands-on practice to learn how to:
  - Navigate the system
  - Change system settings
  - Work with files and folders
  - Manage user accounts
- **Virtual Machine Info**
  - Access: Browser-based or via Remote Desktop Protocol (RDP)
  - IP: `MACHINE_IP`
  - Username: `administrator`
  - Password: `letmein123!`
- Accept the certificate warning when prompted.

📌 Example of RDP configuration:

![RDP Setup](https://github.com/user-attachments/assets/2725e2d4-a007-4a09-9f5b-d7cabc29c58f)

---

## 🪟 Task 2 - Windows Editions

### 📜 Historical Overview
| Version       | Description |
|---------------|-------------|
| Windows XP    | One of the most popular versions |
| Windows Vista | Major UI overhaul; poorly received |
| Windows 7     | Widely adopted in enterprise; set end-of-life early |
| Windows 8.x   | Designed for tablets; short-lived |
| Windows 10    | Long-term support; Home & Pro editions |
| Windows 11    | Released on October 5, 2021 |

### 💡 Key Notes
- Businesses struggled with compatibility during version transitions.
- Each version brought enhancements in usability and security.

> **Note**: The VM runs **Windows Server 2019 Standard**  
> **Windows 10 support ends**: October 14, 2025


---

## 🖼️ Task 3 - The Desktop (GUI)

When logging into a Windows system, the first screen you'll see is the Desktop. It’s part of the Graphical User Interface (GUI).

### 🧩 Main Components of the GUI

1. Desktop
2. Start Menu
3. Search Box (Cortana)
4. Task View
5. Taskbar
6. Toolbars
7. Notification Area

📌 Example of a Windows Desktop:

![Desktop GUI](https://github.com/user-attachments/assets/a7a7786b-d6f3-4788-9f72-e843520b617c)

---

### 🖱️ Desktop Interaction

Right-click on the desktop to see context options like sorting, creating folders, or accessing settings.

![Right Click Menu](https://github.com/user-attachments/assets/94af1403-4bd8-4098-8903-1a1d141dfdba)

From this menu, you can access:

- **Display Settings** for resolution and layout:
  ![Display Settings](https://github.com/user-attachments/assets/0156dc16-e6f0-4670-b0e3-8aa4fae973ce)
  ![Display Window](https://github.com/user-attachments/assets/476375cf-ec1f-4432-b5fd-bbb7e6360040)

- **Personalize** for background, themes, colors:
  ![Personalize](https://github.com/user-attachments/assets/eda50a60-5be8-4bdf-80a5-e93e9f225aff)
  ![Wallpaper Settings](https://github.com/user-attachments/assets/6a09ad43-a1ad-4a81-81b1-98c6f677d46f)

---

### 🪟 Start Menu Overview

The Start Menu provides access to:

- Account settings, Documents, Pictures, Settings, Power
- All installed apps (alphabetical order)
- Recently added programs
- Pinned tiles (right side)

📌 Full Start Menu Example:

![Start Menu Full](https://github.com/user-attachments/assets/2a5d9379-ef9e-422d-8b8d-729c088990cb)

📌 Left Pane Expanded:

![Start Menu Left](https://github.com/user-attachments/assets/0cf8a714-2da2-40ae-800f-f1fd0eec67e6)

📌 Recently Added & App List:

![Start Menu Recent](https://github.com/user-attachments/assets/0747b78e-0d1e-4fd0-9753-abef8f67add3)

📌 Alphabet Grid for Quick Navigation:

![Alphabet Grid](https://github.com/user-attachments/assets/088bc302-336a-463c-92cd-56811d766b77)

📌 Tile Right-Click Options:

![Tile Context Menu](https://github.com/user-attachments/assets/e7403f35-0bc8-45b0-ad02-da3e52cdee8b)

📌 Pinning Apps to Start:

![Pin to Start](https://github.com/user-attachments/assets/c5f52064-2d75-4b24-96cf-d20fcb057a17)

📌 Chrome App Pinned as Tile:

![Chrome Tile](https://github.com/user-attachments/assets/3521969f-7f6d-48e1-bbb4-5e3d52609830)

---

### 📌 Taskbar and Notification Area

- Taskbar shows running programs and pinned apps
- Right-click the taskbar for options:

![Taskbar Context](https://github.com/user-attachments/assets/a6dbf74b-0746-4d1d-8948-6cdebd4c4352)

📌 Hover to Preview App (Tooltip):

![App Preview](https://github.com/user-attachments/assets/91fd179f-1267-4e6d-bc09-d166ae35d10c)

📌 Taskbar Settings:

![Taskbar Settings](https://github.com/user-attachments/assets/11029855-6d48-4f40-a01a-50201da1c60b)

📌 Notification Area Settings:

![Notification Settings](https://github.com/user-attachments/assets/0bc7f541-56bb-4021-9272-e8f6f0e00d94)

---

## 📂 Task 4 - File System

### 🗃️ NTFS (New Technology File System)

NTFS is the modern file system used in Windows. It replaced older systems like FAT16/FAT32 and HPFS.

**Key Features of NTFS:**
- Supports large files over 4GB
- Fine-grained file/folder permissions
- Built-in file/folder compression
- Supports encryption (EFS - Encrypting File System)
- Alternate Data Streams (ADS) for metadata or hidden data

### 🔍 How to Check the File System Type

Right-click on the C: drive → Properties → See "File System: NTFS"

![NTFS File System](https://assets.tryhackme.com/additional/win-fun1/win-file-system.gif)

---

### 🔐 NTFS Permissions

NTFS allows setting specific permissions for files and folders. These permissions control who can access or modify data.

| Permission        | Meaning for Folders                                           | Meaning for Files                                           |
|-------------------|---------------------------------------------------------------|-------------------------------------------------------------|
| Read              | View and list files/subfolders                                | View or access file contents                                |
| Write             | Add files/subfolders                                          | Write to file                                               |
| Read & Execute    | View/list/execute files/subfolders                            | View, access, and execute file                              |
| List Folder Contents | View/list subfolders and files only (inherited)           | N/A                                                         |
| Modify            | Read/write files; delete folders                              | Read/write; delete file                                     |
| Full Control      | All permissions                                               | All permissions                                             |

![NTFS Permission Table](https://github.com/user-attachments/assets/c774934a-ce92-4851-9553-9f6d2fa177f4)

---

### 🔎 Viewing Permissions

To view permissions of a file/folder:

1. Right-click the folder → Properties
2. Go to the **Security** tab
3. Select a user/group to view assigned permissions

![NTFS Folder Security Tab](https://github.com/user-attachments/assets/2efbd849-009a-40e2-baeb-6a998d42e370)

> You can also edit permissions from this tab as an Administrator.

---

## 📁 Task 5 - Windows\System32 Folder

The `C:\Windows` directory contains the core files of the Windows operating system. It doesn’t necessarily have to reside in the `C:` drive, but it usually does by default.

You can access the Windows directory by navigating to:

📌 `This PC > Local Disk (C:) > Windows`

![Windows Directory](https://github.com/user-attachments/assets/082da954-ed2d-43db-bf60-b3cccbe1bb01)

### 📂 The System32 Folder

Located at `C:\Windows\System32`, this folder contains critical system files and utilities.

📌 `This PC > Local Disk (C:) > Windows > System32`

![System32 Folder](https://github.com/user-attachments/assets/122dfe16-27c1-4271-b656-a499fd631cab)

> ⚠️ Warning: Deleting or modifying files in the System32 folder can break the operating system.

This folder includes:
- System tools like `cmd.exe`, `taskmgr.exe`, `regedit.exe`
- Dynamic-link libraries (DLLs)
- Drivers and executables used during system boot and operations

Many command-line tools and services that will be covered in later rooms are located here.


---


---

## 👤 Task 6 - User Accounts, Profiles, and Permissions

Windows supports two main types of user accounts:

| Type           | Description                         |
|----------------|-------------------------------------|
| Administrator  | Full control over system settings and users |
| Standard User  | Limited access; cannot make system-level changes |

---

### 🔍 Finding and Managing Users

You can manage user accounts via the **Other Users** section of Settings.

📌 Search for "Other users" in the Start menu:

![Search Other Users](https://github.com/user-attachments/assets/38b61abd-0969-485c-aef9-b92a6cd85f14)

📌 Open the panel to see the list of accounts and option to add someone:

![Other Users Panel](https://github.com/user-attachments/assets/3d259101-9584-43a1-99d2-f16986d56d29)

📌 Options such as changing account type or removing users are available:

![Change or Remove User](https://github.com/user-attachments/assets/dc4b562f-1dce-402e-9951-a34cc11a2a3d)

📌 Choose the account type from the dropdown:

![Account Type Dropdown](https://github.com/user-attachments/assets/61808709-5361-4d15-a89a-f112ac660526)

---

### 🧑 Creating a User Profile

When a new user logs in for the first time:

1. Windows sets up the profile (this may take a few moments)
2. Default apps are initialized

📌 Profile initialization message:

![User Profile Service](https://github.com/user-attachments/assets/895ba7f3-92b6-4f8c-b798-00c70bf3e2f4)

📌 Personalized settings message:

![Personalized Settings](https://github.com/user-attachments/assets/12898c7a-0443-4f38-a725-fd46ff131be1)

📌 The desktop after profile creation:

![New User Desktop](https://assets.tryhackme.com/additional/win-fun1/win-lusrmgr.gif)


### 🧑‍💻 Account Types
| Type           | Description                         |
|----------------|-------------------------------------|
| Administrator  | Full system access and control      |
| Standard User  | Limited access to system settings   |

- User profiles are located at `C:\Users\{username}`
- Profiles are created automatically on the first login.
- Use `lusrmgr.msc` to manage local users and groups.
- Users inherit permissions from their group memberships.

---


---

## 🔐 Task 7 - User Account Control (UAC)

User Account Control (UAC) is a Windows security feature that prevents unauthorized changes to the operating system.

Even if you're logged in as an administrator, apps that require elevated privileges will prompt for confirmation before executing.

### 🔰 How UAC Works

1. **A program requiring admin privileges** will show a shield icon:
   ![UAC Shield Icon](https://github.com/user-attachments/assets/691006fa-3647-4397-96df-d6946b7dd06b)

2. **When launched**, the UAC prompt appears asking for admin credentials:
   ![UAC Prompt](https://github.com/user-attachments/assets/f95198cf-6cde-4d1f-8018-a24eae3b1d46)

---

### 🔐 File Permissions Example

Right-clicking on an executable file and navigating to the **Security** tab shows which users or groups have permission to execute it.

![UAC Permissions](https://github.com/user-attachments/assets/fae2c34d-2d05-457d-96af-312d67d87b5e)
![UAC Permissions 2](https://github.com/user-attachments/assets/efece080-8d91-4f0d-a187-28f9879bb8b8)

---

These permissions control which accounts are allowed to install or make changes using the program. The UAC prompt adds a confirmation layer to that access.

> 🛡️ UAC helps reduce malware infections by preventing silent installations or unauthorized modifications.


---


---

## ⚙️ Task 8 - Settings vs Control Panel

Windows provides two main interfaces for adjusting system settings:

| Tool           | Description                                    |
|----------------|------------------------------------------------|
| Settings       | Modern interface introduced in Windows 8/10    |
| Control Panel  | Classic, more detailed configuration panel     |

---

### 🧭 Settings App

The Settings app includes categories for network, personalization, system, and more:

![Windows Settings](https://github.com/user-attachments/assets/0d9e90f9-fe20-4084-bf8e-e90f740406ad)

You can access it from the Start Menu:

![Start Menu Settings](https://github.com/user-attachments/assets/2d711bfb-77f3-48cc-be55-f62ebe6f99cd)

---

### 🖥️ Control Panel

Control Panel is the traditional settings interface with categorized sections:

![Control Panel](https://github.com/user-attachments/assets/8cb32c0a-3ba6-4eed-a3ab-f2a68199980e)

Some settings accessed via the Settings app may redirect you to the Control Panel.

---

### 🔄 Example: Network Adapter Settings

1. Open **Settings** → Network & Internet
2. Click **Change adapter options**:

![Change Adapter Option](https://github.com/user-attachments/assets/8491c923-1fd0-4fd0-bcb0-7f329dcb08a5)

3. You will be redirected to **Control Panel > Network Connections**:

![Network Connections - Control Panel](https://github.com/user-attachments/assets/aaae7f89-bee0-4501-acb6-0aedb25e739e)

---

### 🔎 Using Search

If you’re not sure where to find a setting, use the Start Menu’s search:

![Search Wallpaper](https://github.com/user-attachments/assets/3a2c553f-93a4-4cf4-addc-7034ae6d639e)

Which leads to the personalization page:

![Wallpaper Settings](https://github.com/user-attachments/assets/d3482a30-1c54-4429-8588-23efbbbb3b3c)

> 💡 Tip: Use the modern Settings app for general tasks and Control Panel for advanced features.


---


---

## 📊 Task 9 - Task Manager

Task Manager is a built-in Windows utility that allows users to monitor applications, processes, performance, and system resource usage.

---

### 🚀 How to Open Task Manager

- Press `Ctrl + Shift + Esc`
- OR: Right-click the Taskbar → Click **Task Manager**

![Open Task Manager](https://github.com/user-attachments/assets/ad731f15-ea0b-43b4-b26d-8df837c26a4c)

---

### 👀 Basic View

When Task Manager is first opened, it may display only the simple view with a list of running apps.

![Task Manager - Simple View](https://github.com/user-attachments/assets/0093ca4f-40ea-4298-85c3-8a09fbbe8923)

Click **More details** to expand the interface.

---

### 📋 Full Task Manager View

In the full view, you can access:

- **Processes**: Active and background processes
- **Performance**: Real-time usage of CPU, memory, disk, network
- **Users**: Active users and their resource consumption
- **Details / Services**: In-depth info for developers/admins

📌 Example:

![Task Manager - Full View](https://github.com/user-attachments/assets/1404128b-5e31-4d1a-b17a-be974811ae8e)

---

> 💡 Tip: Use Task Manager to close unresponsive programs, check for performance issues, or see what’s consuming memory/CPU.


---

## ✅ Task 10 - Conclusion

This module gave you a practical overview of the Windows OS covering:

- Graphical interface
- File system structure
- User permissions
- System tools

Future topics will include:

- Event Viewer
- Windows Defender & Firewall
- Management consoles and PowerShell scripting

---

## 📚 Additional Learning Resources

- 🔗 [NTFS Technical Reference](https://learn.microsoft.com/en-us/windows/win32/fileio/ntfs-technical-reference)
- 🔗 [User Account Control](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/user-account-control)
- 🔗 [Task Manager Guide](https://www.howtogeek.com/school/using-windows-admin-tools-like-a-pro/lesson2/)
- 🔗 [Alternate Data Streams (MalwareBytes)](https://www.malwarebytes.com/blog/news/2015/02/alternate-data-streams)

---

> ✅ Save this file as `README.md` and include an `/images` folder for screenshots.
