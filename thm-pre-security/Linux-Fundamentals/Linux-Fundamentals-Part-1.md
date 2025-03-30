# 🐧 Linux Fundamentals Part 1 - TryHackMe Room Summary

Welcome to your journey into the Linux operating system — a critical skill for cybersecurity and system administration.

---

## 🧠 Task 1: Introduction

Linux is one of the most widely used operating systems in the world — powering smart cars, Android devices, web servers, supercomputers, and more.

In this room, you'll:
- Run your first Linux commands via a browser-based terminal
- Learn essential file system commands
- Understand how to search and manipulate files

### 🖼️ Image Placeholder  
![Linux Intro](https://github.com/user-attachments/assets/7710b455-314a-4639-86a5-711a7303b88e)

---

## 📜 Task 2: A Bit of Background on Linux

### 🗺️ Where is Linux Used?
- Websites
- Cars and infotainment systems
- POS (Point of Sale) terminals
- Traffic systems and infrastructure

### 🐧 Linux "Flavours"
Linux comes in many "distributions" or variants. In this room, we’ll use **Ubuntu**.

Examples of Linux distros:
- Ubuntu
- Debian
- CentOS
- Arch Linux

---

## 💻 Task 3: Interacting With Your First Linux Machine
## 💻 Task 3: Interacting With Your First Linux Machine (In-Browser)

This room has an Ubuntu Linux machine that you can interact with directly in your browser.

To get started, press the green **Start Machine** button on the top-right.

### 🖼️ Image: Start Machine Button  
![Start Machine Button](https://github.com/user-attachments/assets/03fcaafd-7cbb-47b6-ba03-dc2f288ea07e)

Once the machine is deployed, you’ll see the active machine card with its IP address and timer:

### 🖼️ Image: Active Machine Panel  
![Active Machine Info](https://github.com/user-attachments/assets/615d6df3-4a3d-4b61-933d-84b6df843a0d)

You’ll be able to use a full Ubuntu terminal right in your browser, like this:

```bash
tryhackme@ip-10-10-234-200:~$

---

## 🧪 Task 4: Running Your First Few Commands

The terminal may seem scary at first, but you’ll soon be comfortable with it.

| Command | Description                        |
|---------|------------------------------------|
| `echo`  | Print text to the screen           |
| `whoami`| Show current logged-in username    |

```bash
tryhackme@linux1:~$ echo "Hello Friend!"
tryhackme@linux1:~$ whoami
```

---

## 📂 Task 5: Interacting With the Filesystem

Learn how to list, navigate, and read files.

| Command | Full Name               |
|---------|-------------------------|
| `ls`    | List files              |
| `cd`    | Change directory        |
| `cat`   | Concatenate/read files  |
| `pwd`   | Print working directory |

Example usages:

```bash
# List files
ls

# Change into Pictures folder
cd Pictures
ls

# View contents of a file
cat Documents/todo.txt

# Show full path of current location
pwd
```

---

## ⚙️ Task 7: An Introduction to Shell Operators

Shell operators are used to control command behavior.

| Operator | Description |
|----------|-------------|
| `&`      | Run command in background |
| `&&`     | Run next command only if previous succeeded |
| `>`      | Redirect output to a file (overwrite) |
| `>>`     | Append output to a file |

### Examples:

```bash
echo hey > welcome
cat welcome
# Output: hey

echo hello >> welcome
cat welcome
# Output:
# hey
# hello
```

---

## 🧾 Task 8: Conclusions & Summaries

✅ In this room, you’ve learned:

- Why Linux is widely used
- How to access your first Linux machine
- Fundamental commands (`ls`, `cd`, `cat`, `pwd`)
- Shell operators for advanced usage
- How to navigate and interact with the Linux filesystem

Keep practicing — you’ll become comfortable quickly!

---

## 👉 Task 9: Proceed to Part 2

Continue learning in [Linux Fundamentals Part 2](https://tryhackme.com/room/linuxfundamentalspart2)
