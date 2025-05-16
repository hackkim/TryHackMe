# 🧠 TryHackMe: Network Security Module — Passive Reconnaissance

This document summarizes **Tasks 1 through 7** from the TryHackMe "Network Security" module, focusing on **Passive Reconnaissance**. You’ll learn how to gather information on a target without direct interaction using tools like `whois`, `nslookup`, `dig`, and online services such as `DNSDumpster` and `Shodan.io`.

---

## 🔹 Task 1: Introduction

This room covers:

1. Passive Reconnaissance  
2. Active Reconnaissance  
3. Nmap Live Host Discovery  
4. Nmap Basic Port Scans  
5. Nmap Advanced Port Scans  
6. Nmap Post Port Scans  
7. Protocols and Servers  
8. Protocols and Servers 2  
9. Network Security Challenge

Tools for passive reconnaissance introduced here include:

- `whois`: WHOIS record lookup
- `nslookup` and `dig`: DNS querying tools
- `DNSDumpster`: Subdomain and DNS intelligence
- `Shodan.io`: Internet-connected device search engine

---

## 🔹 Task 2: Passive vs Active Recon

**Passive Reconnaissance**:
- Gathers data from public sources without engaging the target
- Examples:
  - DNS queries
  - News articles
  - Job postings

![Passive Reconnaissance](https://github.com/user-attachments/assets/0bba220a-a366-4097-96ba-0bf2d92df8be)

**Active Reconnaissance**:
- Involves direct interaction with the target systems
- Examples:
  - Connecting to services like HTTP, FTP
  - Social engineering
  - Physical reconnaissance

⚠️ Active recon may raise alarms or result in legal consequences if not authorized.

![Active Reconnaissance](https://github.com/user-attachments/assets/679f83ee-c230-4fbe-abb7-af4a0ddbc16b)

---

## 🔹 Task 3: Whois

**WHOIS** is a TCP protocol (port 43) used to retrieve domain registration details.

```bash
whois tryhackme.com
```

You can learn:
- Registrar & expiration dates
- Name servers
- Registrant contact info (if not redacted)

WHOIS data can inform social engineering vectors or help scope technical vulnerabilities (e.g., DNS misconfigurations).

---

## 🔹 Task 4: nslookup & dig

### `nslookup` Usage:

```bash
nslookup -type=A tryhackme.com
nslookup -type=MX tryhackme.com 1.1.1.1
```

### `dig` Usage:

```bash
dig tryhackme.com MX
dig @1.1.1.1 tryhackme.com TXT
```

| Query Type | Description        |
|------------|--------------------|
| A          | IPv4 address       |
| AAAA       | IPv6 address       |
| MX         | Mail servers       |
| TXT        | SPF, verification  |
| CNAME      | Canonical names    |

`dig` returns more detail including TTL, making it more suitable for deeper DNS analysis.

---

## 🔹 Task 5: DNSDumpster

[DNSDumpster](https://dnsdumpster.com) is a free online tool that maps a domain’s DNS information:

- Subdomains (e.g., blog.tryhackme.com)
- DNS and MX records
- TXT/SPF records
- Visual diagrams of relationships
- IP address geolocation

### 📄 Tabular Output Example:

![DNSDumpster Table Output](https://github.com/user-attachments/assets/bde3c02e-62c3-45a2-86cb-dc632be2be8d)

### 🗺️ Visual DNS Map:

![DNSDumpster Visual Graph](https://github.com/user-attachments/assets/4f730459-38b9-4174-8202-3bc59f41b148)

### 🗺️ Visual DNS Map (2):

Below is another style of DNS visualization showing authoritative name servers, IP addresses, email servers, and subdomain structure including hosting provider metadata.

![DNSDumpster Alternate Graph](./eb95e62815b6ace3c823fd0159884731.jpeg)

---

## 🔹 Task 6: Shodan.io

[Shodan.io](https://www.shodan.io) indexes metadata of devices exposed on the internet (e.g., webcams, routers, servers).

It provides:
- Server banner info
- Open ports
- TLS/SSL configurations
- Hostnames & geographic data

### 📷 Example: `tryhackme.com`

- IP: 54.220.229.192
- Location: Dublin, Ireland (Amazon EC2)
- Server: `nginx/1.14.0 (Ubuntu)`
- Status: `301 Moved Permanently`

![Shodan tryhackme.com result](https://github.com/user-attachments/assets/caa39afa-9ca3-4d89-8e3c-a8960ebf73de)

Shodan allows you to identify vulnerabilities based on outdated software or services exposed to the public.

---

## 🔹 Task 7: Summary

| Purpose                        | Commandline Example                            |
|-------------------------------|--------------------------------------------------|
| WHOIS lookup                  | `whois tryhackme.com`                          |
| A record with nslookup        | `nslookup -type=A tryhackme.com`              |
| MX record with custom server  | `nslookup -type=MX tryhackme.com 1.1.1.1`     |
| TXT record with nslookup      | `nslookup -type=TXT tryhackme.com`            |
| A record with dig             | `dig tryhackme.com A`                          |
| MX record with dig            | `dig @1.1.1.1 tryhackme.com MX`               |
| TXT record with dig           | `dig tryhackme.com TXT`                        |

---

✅ **Conclusion**  
Mastering passive reconnaissance is essential for both red and blue teams. The ability to gather useful intelligence without alerting the target is powerful, and tools like `whois`, `dig`, `DNSDumpster`, and `Shodan` make it highly accessible and effective.
