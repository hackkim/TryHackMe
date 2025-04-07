# 🐧 TryHackMe - Linux Shells (Full Markdown Documentation)

Welcome to the **Linux Shells** room on TryHackMe. In this room, you’ll explore what a shell is, how it differs from a GUI, learn to use common shell commands, compare different shell types (like Bash, Zsh, and Fish), and even write your own shell scripts.

---

## 🐚 Task 1 - Introduction to Linux Shells

### 💡 Why use the CLI?

Most people use the Graphical User Interface (GUI) to perform operations. However, using the Command Line Interface (CLI) through a **shell** is much more powerful and flexible.

**Analogy:**
- GUI = Ordering food at a restaurant
- CLI = Cooking the food yourself
- Shell = Assistant that helps you in the kitchen with recipes

Using CLI in Linux gives you:
- Greater control
- Better performance
- Automation capabilities

### 🎯 Learning Objectives
- Interact with Linux shell
- Use basic shell commands
- Explore types of Linux shells
- Write shell scripts for automation

**🧠 Prerequisite:** Complete the Linux Fundamentals module before proceeding.

---

![Linux Shells Intro](https://github.com/user-attachments/assets/6ad15f52-8f67-4c17-9fbf-a54045452f50)

## 🔌 Task 2 - How to Interact With a Shell?

### 🚀 Step 1: Start the Virtual Machine
- Press **Start Machine**
- If not visible, click **Show Split View**

### 💻 Step 2: Connect via SSH
![SSH Credentials](https://github.com/user-attachments/assets/b696ee15-f506-4867-b450-3b459b52cd2d)

```bash
ssh user@MACHINE_IP
# Password: user@Tryhackme
```

### 🖥️ Step 3: Shell Prompt
You’ll see the shell prompt like:
```bash
user@ubuntu:~$
```

This is your **interactive shell**—likely Bash.

---

### 🧪 Common Linux Shell Commands

| Command | Description |
|---------|-------------|
| `pwd`   | Print Working Directory |
| `cd`    | Change Directory |
| `ls`    | List files in a directory |
| `cat`   | Display contents of a file |
| `grep`  | Search for text in a file |

**Examples:**
```bash
pwd
cd Desktop
ls
cat file.txt
grep THM dictionary.txt
```

**Output:**
```
The flag is THM
```

---

## 🐚 Task 3 - Types of Linux Shells

Linux offers a variety of shell types—each with unique capabilities.

### 🔍 How to Check Which Shell You're Using
```bash
echo $SHELL
```

### 📃 List All Installed Shells
```bash
cat /etc/shells
```

**Output:**
```
/bin/sh
/bin/bash
/usr/bin/zsh
/usr/bin/fish
...
```

### 🔄 Switch to Another Shell (Temporarily)
```bash
zsh
```

### ♻️ Set Shell as Default (Permanently)
```bash
chsh -s /usr/bin/zsh
```

---

### 🔎 Comparison: Bash vs Zsh vs Fish

| Feature               | Bash            | Zsh                    | Fish                        |
|-----------------------|------------------|------------------------|-----------------------------|
| Full Name             | Bourne Again SH  | Z Shell                | Friendly Interactive Shell  |
| Default in Linux?     | Yes              | No                     | No                          |
| Scripting             | ✅ Great         | ✅ Excellent            | ⚠️ Limited                  |
| Tab Completion        | Basic            | Advanced with Plugins  | Contextual and Friendly     |
| Syntax Highlighting   | ❌ Not Native    | ✅ With Plugins         | ✅ Built-in                 |
| Customization         | Limited          | High (oh-my-zsh)       | Moderate                    |
| Spell Correction      | ❌               | ✅                      | ✅                          |

---

## ✍️ Task 4 - Shell Scripting and Components

Shell scripting automates repetitive tasks by combining commands in a script file.

---

### 📝 Step 1: Create a Script
```bash
nano hello.sh
```

```bash
#!/bin/bash
echo "Hello, what is your name?"
read name
echo "Welcome, $name!"
```

---

### 🔐 Step 2: Make It Executable
```bash
chmod +x hello.sh
```

---

### ▶️ Step 3: Run It
```bash
./hello.sh
```

---

### 🔁 Using Loops in Scripts
```bash
#!/bin/bash
for i in {1..5}
do
  echo "Number: $i"
done
```

---

### ✅ Conditional Statements (if/else)
```bash
#!/bin/bash
echo "Enter your name:"
read name

if [ "$name" = "Stewart" ]; then
  echo "Welcome, Stewart!"
else
  echo "Access Denied!"
fi
```

---

### 💬 Comments in Scripts
Use comments for documentation and understanding:
```bash
# This script asks for a name and welcomes the user.
#!/bin/bash
read name
echo "Hello $name!"
```

---

## 🗝️ Task 5 - The Locker Script

A simple authentication script using variables, conditionals, and loops:

```bash
#!/bin/bash

username=""
companyname=""
pin=""

for i in {1..3}; do
  if [ "$i" -eq 1 ]; then
    echo "Enter Username:"
    read username
  elif [ "$i" -eq 2 ]; then
    echo "Enter Company:"
    read companyname
  else
    echo "Enter PIN:"
    read pin
  fi
done

if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
  echo "Authentication Successful. Access granted!"
else
  echo "Authentication Failed!"
fi
```

---

## 🧪 Task 6 - Practical Exercise

### 🧭 Objective
Find a hidden flag inside `/var/log` using a pre-written script on the machine.

### 🪪 Become Root
```bash
sudo su
```

> Use password: `user@Tryhackme`

### 🔍 Script Target
- Flag: `thm-flag01-script`
- Directory: `/var/log`
- Edit the script to insert values inside the empty quotes: `""`

---

## ✅ Task 7 - Conclusion

### 🎓 What You’ve Learned
- The power of CLI vs GUI
- The role of Shells in Linux
- Bash vs Zsh vs Fish comparison
- Writing reusable and secure scripts
- Practical exercise using a real script

---

> 🚀 Now you’re ready to go beyond the GUI and embrace the true power of Linux. Keep scripting, keep learning, and remember: automation is power! 🧠⚙️🐧
