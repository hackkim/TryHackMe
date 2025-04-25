# 🌐 TryHackMe - Web Hacking Path (Detailed Overview)

This markdown provides a structured summary of the **Web Hacking Path** on TryHackMe.  
It introduces web technologies, client/server interactions, common vulnerabilities, and essential tools for modern web application penetration testing.

---

## 🖼️ Visual Overview

![Web Hacking Overview](https://github.com/user-attachments/assets/019d4aa3-e973-486a-94e4-09eb63261601)

> An overview of the core learning modules in the Web Hacking path by TryHackMe.

---

## 🛠️ Modules Included

### 1. 🧩 Web Application Basics

![Web Application Basics](https://github.com/user-attachments/assets/c7c977b7-2fab-4f3b-a68f-36b4d1bd0b3f)

#### 📚 What You’ll Learn:
- How web applications work
- HTTP request/response flow
- HTTP methods: `GET`, `POST`, `PUT`, `DELETE`
- Status codes: `200 OK`, `302 Found`, `403 Forbidden`, `500 Internal Server Error`
- Headers and cookies
- Web architecture: client-server model

#### 📌 Why It Matters:
Understanding web basics is essential before learning exploitation. This module lays the groundwork.

---

### 2. 🖱️ JavaScript Essentials

![JavaScript Essentials](https://github.com/user-attachments/assets/c2ebf784-fbdf-4a22-9603-acd27fbb5297)

#### 📚 What You’ll Learn:
- JavaScript syntax and execution
- DOM manipulation
- Client-side validation and logic
- How JavaScript is used in modern websites
- Common vulnerabilities:
  - DOM-based XSS
  - Client-side injection

#### 📌 Why It Matters:
Many web vulnerabilities today exploit JavaScript. You’ll need to understand JS to spot and exploit them.

---

### 3. 🧮 SQL Fundamentals

![SQL Fundamentals](https://github.com/user-attachments/assets/80de32c7-fee7-4da1-a355-98ec01f48a44)

#### 📚 What You’ll Learn:
- SQL basics: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
- Query filtering: `WHERE`, `LIKE`, `ORDER BY`
- Table relationships and joins
- How input is processed and queried from databases

#### 📌 Why It Matters:
SQL Injection (SQLi) is a top web vulnerability. Knowing SQL helps understand how to exploit and prevent SQLi.

---

### 4. 🧪 Burp Suite: The Basics

![Burp Suite: The Basics](https://github.com/user-attachments/assets/6a49c2c9-586b-4e9b-b497-e84991ae88de)

#### 📚 What You’ll Learn:
- Introduction to Burp Suite (Community Edition)
- Proxy configuration (browser ↔ Burp)
- Tools overview:
  - Repeater (manual request testing)
  - Intruder (automated attacks)
  - Decoder (decode/encode data)
  - Comparer (response comparison)

#### 📌 Why It Matters:
Burp Suite is the **most used tool** in web pentesting. Mastering it is a must for bug bounty hunters and professionals.

---

### 5. 🛡️ OWASP Top 10 - 2021

![OWASP Top 10 - 2021](https://github.com/user-attachments/assets/f710f84a-ec28-44fc-8507-7c22d42e0387)

#### 📚 What You’ll Learn:
- The 10 most critical web vulnerabilities:
  1. Broken Access Control
  2. Cryptographic Failures
  3. Injection (e.g. SQLi, XSS)
  4. Insecure Design
  5. Security Misconfiguration
  6. Vulnerable and Outdated Components
  7. Identification and Authentication Failures
  8. Software and Data Integrity Failures
  9. Logging and Monitoring Failures
  10. Server-Side Request Forgery (SSRF)

#### 📌 Why It Matters:
The OWASP Top 10 is an industry-standard checklist. You’ll learn to detect and exploit each of these with hands-on labs.

---

## 🚀 Learning Objectives

By completing this path, you will:

- Understand how web applications function at the protocol level
- Identify and exploit common web vulnerabilities
- Learn how to analyze and manipulate client-side and server-side behaviors
- Use Burp Suite and manual testing techniques
- Be well-prepared for **web-focused CTFs** and **bug bounty** programs

---

## 🧠 Who Should Learn This?

- 🔰 Complete beginners in web hacking
- 💼 Cybersecurity students and trainees
- 🐞 Aspiring bug bounty hunters
- 👩‍💻 Developers who want to understand how attackers think

---

## 📚 Additional Resources

- 🔗 [TryHackMe Web Hacking Path](https://tryhackme.com/path/preview/web-hacking)
- 🔗 [OWASP Top 10 Official Project](https://owasp.org/www-project-top-ten/)
- 📖 [PortSwigger Web Security Academy](https://portswigger.net/web-security)

---

## ✅ Completion Outcome

Once you complete this path, you’ll:
- Have a strong understanding of web fundamentals
- Know how to use tools like Burp Suite effectively
- Be able to manually test for vulnerabilities like XSS, SQLi, IDOR, SSRF
- Be ready to move on to intermediate/advanced web hacking rooms
