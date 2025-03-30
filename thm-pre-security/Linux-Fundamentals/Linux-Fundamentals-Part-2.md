# 🐧 Linux Fundamentals Part 2 - TryHackMe Room Summary

Continue your Linux learning journey with Part 2! In this room, you will learn how to remotely access Linux systems, explore file system interactions in depth, and understand Linux permissions and structure.

---

## 🧠 Task 1: Introduction

Welcome to Part 2 of the Linux Fundamentals series. You’ll apply what you learned in Part 1 and begin learning how to:
- Log in to remote machines using **SSH**
- Use **flags and arguments** with commands
- **Copy, move, delete** files and folders
- Understand **file and folder permissions**
- Run your first scripts and executables

### 🖼️ Image  
![Linux Fundamentals Title](https://github.com/user-attachments/assets/472b7ba3-d423-42d8-9734-729f767dbdc1)

---

## 🔐 Task 2: Accessing Your Linux Machine Using SSH

You'll deploy two machines:
- A **Linux target machine**
- The **TryHackMe AttackBox**

### What is SSH?
**SSH (Secure Shell)** is an encrypted protocol used to log in and execute commands on remote systems.

### 🖼️ Image  
![SSH Communication Flow](https://github.com/user-attachments/assets/1c9028ad-3453-40da-acef-9e322c75da0b)

To log in:
```bash
ssh tryhackme@<IP_ADDRESS>
# Password: tryhackme
```

The AttackBox terminal can be accessed via browser and is used to SSH into the target machine.

### 🖼️ Image  
![Linux Machine Info Card](https://github.com/user-attachments/assets/f3e48280-b83c-483d-a45b-b2afd4e884d3)

### 🖼️ Image  
![Start AttackBox Button](https://github.com/user-attachments/assets/b458d952-def1-404b-8f45-1031d79b7619)

### 🖼️ Image  
![SSH Terminal Session](https://github.com/user-attachments/assets/3fc3fb59-d10f-4233-bb05-272b329e4617)

---

## 🧩 Task 3: Introduction to Flags and Switches

Most commands support **flags/switches** to modify behavior.

Examples using `ls`:
```bash
ls        # list files
ls -a     # show hidden files
ls --help # show help for options
man ls    # open manual page
```

Flags often use `-` (short) or `--` (long) formats.

---

## 📂 Task 4: Filesystem Interaction Continued

Learn to create, move, copy, and delete files and folders.

| Command | Full Name         | Purpose                    |
|---------|-------------------|----------------------------|
| `touch` | Touch             | Create a blank file        |
| `mkdir` | Make Directory    | Create a folder            |
| `cp`    | Copy              | Copy files/folders         |
| `mv`    | Move              | Move or rename             |
| `rm`    | Remove            | Delete files/folders       |
| `file`  | File Identifier   | Determine file type        |

### Examples:
```bash
touch note
mkdir myfolder
rm -R myfolder
cp note note2
mv note2 note3
file note
```

---

## 🔐 Task 5: Permissions 101

Linux uses permission bits to control access:

| Symbol | Meaning     |
|--------|-------------|
| `r`    | Read        |
| `w`    | Write       |
| `x`    | Execute     |

Switch users with:
```bash
su user2         # switch user
su -l user2      # full login shell
```

Use `ls -l` or `ls -lh` to view permission details.

---

## 📁 Task 6: Common Directories

### `/etc`
System configuration files, including:
- `sudoers`
- `passwd`
- `shadow`

### `/var`
Stores variable data like:
- Logs (`/var/log`)
- Databases

### `/root`
Home directory for the root user

### `/tmp`
Temporary files, auto-cleared on reboot — writable by any user.

---

## 📚 Task 7: Summary

You learned:
- How to SSH into a Linux machine
- Use flags, switches, and manual pages
- File creation, deletion, and management
- Linux file permissions and user switching
- Critical root directories and their purpose

Practice and repetition are key to mastering Linux!

---

## 🚀 Task 8: Continue to Part 3

Move on to [Linux Fundamentals Part 3](https://tryhackme.com/room/linuxfundamentalspart3)
