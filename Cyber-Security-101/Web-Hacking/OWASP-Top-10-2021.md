# OWASP Top 10 - 2021

---

## Task 1 - Introduction

![OWASP Logo](https://github.com/user-attachments/assets/0c2693a6-71b0-4b0d-9132-31739496c7d3)

The OWASP Top 10 represents the most critical security risks facing web applications today.  
This room explains each vulnerability in detail, how it can be exploited, and how it can be prevented.  
No previous cybersecurity knowledge is required.

Topics covered:
- Broken Access Control
- Cryptographic Failures
- Injection
- Insecure Design
- Security Misconfiguration
- Vulnerable and Outdated Components
- Identification and Authentication Failures
- Software and Data Integrity Failures
- Security Logging & Monitoring Failures
- Server-Side Request Forgery (SSRF)

---

## Task 2 - Accessing Machines

![Accessing Machines](https://github.com/user-attachments/assets/f5fc0da1-537d-47c4-a21d-a9748f0d1d13)

To interact with practice machines:
- Use **OpenVPN** to connect your device
- Or launch **AttackBox** (browser-based)

Use the **Start Machine** button to deploy machines.

---

## Task 3 - Broken Access Control

![Broken Access Control](https://github.com/user-attachments/assets/fbee40d7-6733-4b3d-912a-7d1a04b4fdd7)

Broken Access Control occurs when users can access data, pages, or functions they shouldn't.

Real-World Example:
- In 2019, private YouTube video frames were accessible due to missing access controls.

Impact:
- Unauthorized data exposure
- Escalation of user privileges

---

## Task 4 - IDOR (Insecure Direct Object Reference)

![IDOR Example](https://github.com/user-attachments/assets/75aae91e-e2f6-4144-96fc-fd6312c046f4)
![IDOR Attack](https://github.com/user-attachments/assets/3df27b88-8388-4755-985e-35ac47c10599)

Applications that expose internal object identifiers (e.g., user IDs) without validation are vulnerable.

Example:
- Changing a URL parameter like `id=123` to `id=124` to access another user's data.

---

## Task 5 - Cryptographic Failures

Sensitive data (like passwords, credit cards) must be protected via strong encryption.

Common mistakes:
- Not using HTTPS
- Weak cryptographic algorithms
- Unencrypted database storage

---

## Task 6 - Flat-File Database Vulnerability

Databases like **SQLite** can be exposed if stored under web-accessible directories.

Attack Steps:
```bash
sqlite3 database.db
.tables
PRAGMA table_info(customers);
SELECT * FROM customers;
```

---

## Task 7 - Cracking Password Hashes

![Crackstation Interface](https://github.com/user-attachments/assets/b28208a9-18bc-4068-951c-08e55b35b5fb)
![Crackstation Interface](https://github.com/user-attachments/assets/7677bb00-467e-45d0-be74-a7057ce8037c)

Extracted password hashes (especially weak MD5 hashes) can be cracked using online tools like Crackstation.

Example:
- MD5 hash `5f4dcc3b5aa765d61d8327deb882cf99` = password: **password**

---

## Task 8 - Cryptographic Failures (Challenge)

Hands-on challenge:
- Locate exposed database
- Crack hashes to retrieve user credentials

---

## Task 9 - Injection Vulnerabilities

Injection occurs when user input is misinterpreted as code.

Common types:
- SQL Injection
- Command Injection

Prevention:
- Input validation
- Parameterized queries

---

## Task 10 - Command Injection

![Cowsay Command Flow](https://github.com/user-attachments/assets/914db106-fd4f-41c9-89f9-e80f25bb4376)
![Inline Command Example](https://github.com/user-attachments/assets/1c583a36-60ed-43a5-8a71-1d621e553dc2)
![Command Injection Result](https://github.com/user-attachments/assets/66f28573-433a-4af7-b25c-221d38622882)

Command Injection happens when unsanitized input is passed to system-level functions (e.g., `passthru()` in PHP).

Attack Example:
```bash
$(whoami)
```

---

## Task 11 - Insecure Design

![insecure-password-reset-single](https://github.com/user-attachments/assets/3824a75e-d4de-472a-afbd-42a32351f735)
![insecure-password-reset-single](https://github.com/user-attachments/assets/c5afd27b-c211-43ac-bc15-d9e96e73d356)

Design flaws arise when threat modeling is missing early in the SDLC.

Example:
- Instagram OTP brute-force was possible using thousands of IP addresses to bypass rate-limits.

---

## Task 12 - Security Misconfiguration

![werkzeug-debug-console](https://github.com/user-attachments/assets/b31edb21-171a-4ce0-8d53-5041f3633f72)


Examples include:
- Leaving admin interfaces exposed
- Using default passwords
- Unnecessary services enabled

Case: Werkzeug debug console left exposed, leading to full remote code execution.

---

## Task 13 - Vulnerable and Outdated Components

Using old, unpatched software makes exploitation easier.

Example:
- Nostromo 1.9.6 web server with a known RCE vulnerability.

---

## Task 14 - Exploiting Outdated Components

![nostromo-default-page](https://github.com/user-attachments/assets/a3491840-f113-46e2-8fe7-b6dce4aadda9)
![nostromo-exploitdb-results](https://github.com/user-attachments/assets/3a73dabe-6872-4b5c-95bf-e81c45d1742e)
![nostromo-exploit-error](https://github.com/user-attachments/assets/15cd2f2e-1541-4582-a870-70bb876f548b)
![nostromo-exploit-code-comment](https://github.com/user-attachments/assets/0d24336e-e71d-44fa-a842-570c2a4a4888)
![nostromo-rce-success](https://github.com/user-attachments/assets/cf441c45-1c11-450c-b8b4-892a457863f6)

Steps:
1. Identify the software and version.
2. Search public databases (e.g., Exploit-DB).
3. Adapt existing exploits if necessary.

---

## Task 15 - Identification and Authentication Failures

Common issues:
- Weak passwords allowed
- No rate limiting
- Predictable session identifiers

Mitigations:
- Strong password policies
- MFA implementation
- Session management best practices

---

## Task 16 - Exploiting Authentication Flaws

![data-leak-scenario](https://github.com/user-attachments/assets/3e6384c0-4026-4f46-8a3c-05e979d7600b)

Example:
- Bypass username validation by adding whitespace (` admin`) during registration.

Result:
- Access an existing account.

---

## Task 17 - Software and Data Integrity Failures

Software or data can be tampered with if integrity checks are missing.

Solutions:
- Use checksums (MD5, SHA256)
- Use Subresource Integrity (SRI) when loading scripts externally.

---

## Task 18 - Using Subresource Integrity

![winscp-file-hashes](https://github.com/user-attachments/assets/7dc4f33d-3684-4fe2-ab8a-1917a29782bb)
![hash_check_terminal](https://github.com/user-attachments/assets/cdb0e808-d2c5-445f-837b-567b2d067431)

Proper HTML example with SRI:
```html
<script src="https://example.com/script.js" integrity="sha384-abc123..." crossorigin="anonymous"></script>
```

---

## Task 19 - Data Integrity Failures in Sessions

![external_jquery_script](https://github.com/user-attachments/assets/5cbd69d0-42f2-40db-a53e-9e94db42301a)

JWTs (JSON Web Tokens) can ensure session integrity.

Structure:
- Header
- Payload
- Signature

JWT Signature ensures payload data has not been tampered with.

---

## Task 20 - JWT None Attack

![cookie_user_manipulation](https://github.com/user-attachments/assets/ec81b4a5-0df1-45dc-8909-47aebab0c1ce)
![jwt_token_structure](https://github.com/user-attachments/assets/6738cd07-a605-4151-985b-3cb2e688813c)
![jwt_none_attack](https://github.com/user-attachments/assets/9041e888-2276-433e-89b9-10698a373044)

Older JWT libraries allowed bypassing verification by:
- Setting `alg: none` in the header
- Removing the signature part

Attackers could modify user roles easily.

---

## Task 21 - Security Logging and Monitoring Failures

Good logging practices include:
- Timestamping all requests
- Recording IP addresses
- Storing logs securely

Lack of monitoring allows attackers to remain undetected.

---

## Task 22 - Server-Side Request Forgery (SSRF)

![ssrf_diagram](https://github.com/user-attachments/assets/9cbfc46f-88bd-4e98-a07e-08aa629c031c)
![ssrf_exploit_netcat](https://github.com/user-attachments/assets/a40817d1-d1b4-414e-80e0-98926a71fef0)

SSRF vulnerabilities allow attackers to make requests from the server itself.

Risks:
- Internal network scanning
- Access to internal-only services (e.g., AWS metadata)
- Possible escalation to RCE

---

## Task 23 - What Next?

Congratulations!  
You now understand the OWASP Top 10 - 2021 vulnerabilities in depth.

Next Steps:
- Enroll in Beginner Cybersecurity Pathways
- Practice more vulnerability exploitation labs
- Start applying these concepts in real-world assessments!

---
