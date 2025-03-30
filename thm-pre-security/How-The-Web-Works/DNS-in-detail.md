# 🌐 DNS Fundamentals - TryHackMe Room Summary

This document summarizes the key concepts from TryHackMe's DNS learning path — including what DNS is, how it works, its structure, record types, and how to query it.

---

## 🧠 Task 1: What is DNS?

**DNS (Domain Name System)** is like the phonebook of the internet. It helps convert human-friendly domain names (like `tryhackme.com`) into machine-readable IP addresses (like `104.26.10.229`).

- Every device on the internet has a unique **IP address**.
- Remembering IPs is hard — DNS lets us use easy-to-remember **domain names** instead.
- Example:  
  `tryhackme.com` ➝ `104.26.10.229`

---

## 🏛️ Task 2: Domain Hierarchy

Domains follow a hierarchical structure.

![Domain Hierarchy](https://github.com/user-attachments/assets/f10745f4-4513-42f7-80b4-ef67943122c9)

### 🔹 TLD (Top-Level Domain)

- The rightmost part of a domain.  
  Examples: `.com`, `.org`, `.net`, `.uk`, `.kr`
- Two types:
  - **gTLD (Generic Top-Level Domain)**: `.com`, `.org`, `.edu`
  - **ccTLD (Country Code Top-Level Domain)**: `.uk`, `.jp`, `.ca`

### 🔹 Second-Level Domain

- The main domain name, located directly to the left of the TLD.  
  Example: `tryhackme` in `tryhackme.com`
- Rules:
  - Up to 63 characters
  - Only lowercase letters (a-z), numbers (0-9), and hyphens (-)
  - Cannot start or end with hyphens
  - No consecutive hyphens allowed

### 🔹 Subdomain

- Appears to the left of the Second-Level Domain  
  Example: `admin` in `admin.tryhackme.com`
- You can use multiple subdomains:  
  Example: `jupiter.servers.tryhackme.com`
- The full domain name must be 253 characters or less.

---

## 📁 Task 3: DNS Record Types

DNS supports various record types. Here are the most common ones:

| Record Type | Description |
|-------------|-------------|
| **A**       | Maps a domain to an IPv4 address (e.g., `104.26.10.229`) |
| **AAAA**    | Maps a domain to an IPv6 address (e.g., `2606:4700:20::681a:be5`) |
| **CNAME**   | Points a domain to another domain name |
| **MX**      | Specifies the mail servers for a domain (includes priority) |
| **TXT**     | Stores text-based data (e.g., domain ownership verification, email authentication info) |

---

## 🔄 Task 4: Making a DNS Request

### DNS Resolution Process:

![DNS Resolution Flow](https://github.com/user-attachments/assets/5e187532-797a-4608-83af-92559984bc8a)

1. **Local Cache Check**  
   - Your computer checks its local DNS cache first.
   - If an entry exists, it returns immediately.

2. **Recursive DNS Server Request**  
   - Typically provided by your ISP (or configured manually).
   - If the record isn’t cached here, it queries further.

3. **Root DNS Servers**  
   - These servers direct the request to the appropriate TLD server (e.g., `.com`).

4. **TLD Server**  
   - The TLD server provides the location of the **Authoritative Name Server**.

5. **Authoritative DNS Server**  
   - Holds the actual DNS records for the domain.
   - Responds with the DNS record (A, MX, etc.) back to the Recursive DNS Server.

📌 **TTL (Time To Live)**: DNS responses include a TTL value (in seconds), which tells how long the response should be cached before requesting again.

---

## 🛠️ Task 5: Practical - DNS Lookup Tools

### 🔧 Useful DNS Commands (CLI):

```bash
# Lookup A record
nslookup tryhackme.com

# Lookup MX record
nslookup -query=MX tryhackme.com

# Lookup TXT record
nslookup -query=TXT tryhackme.com

# Use dig (Linux/macOS)
dig tryhackme.com

# Use host command
host -t MX tryhackme.com
```
