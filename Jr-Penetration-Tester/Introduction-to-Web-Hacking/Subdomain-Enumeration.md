# 🌐 Subdomain Enumeration

---

## Task 1: Introduction to Subdomain Enumeration

**Subdomain Enumeration** involves identifying valid subdomains associated with a particular domain. It significantly expands the attack surface, uncovering potential vulnerabilities in websites or web applications that may be overlooked or intentionally hidden.

**Methods of Subdomain Enumeration:**

* **Brute Force Enumeration:** Systematically testing common subdomain names.
* **OSINT (Open-Source Intelligence):** Leveraging publicly available information sources.
* **Virtual Host Enumeration:** Identifying subdomains by modifying HTTP host headers.

---

## Task 2: OSINT - SSL/TLS Certificates (crt.sh)

When SSL/TLS certificates are issued by Certificate Authorities (CA), these certificates are logged publicly via Certificate Transparency (CT) logs. Attackers and security researchers can query these logs to discover previously issued certificates, revealing associated subdomains.

### Steps to Use crt.sh:

1. Access [crt.sh](https://crt.sh).
2. Search for the target domain (e.g., `tryhackme.com`).
3. Identify certificates logged on specific dates, noting down relevant subdomains.

**Example:**

```
Certificate: *.tryhackme.com  
Logged: 2020-12-26  
```

---

## Task 3: OSINT - Search Engines (Google Dorking)

Search engines index vast amounts of data, making them valuable tools for discovering hidden or obscure subdomains.

**Google Dorking Example:**

```text
site:*.tryhackme.com -site:www.tryhackme.com
```

* `site:` focuses search results on a specific domain.
* `-site:` excludes certain subdomains, enhancing search precision.

---

## Task 4: DNS Bruteforce (dnsrecon)

DNS Bruteforce is the practice of systematically checking large sets of common subdomains against a target domain to discover hidden subdomains.

**Example using dnsrecon:**

```bash
dnsrecon -d domain.com -w wordlist.txt
```

* `-d` specifies the target domain.
* `-w` specifies the wordlist of potential subdomains to test.

---

## Task 5: OSINT - Sublist3r (Automated Subdomain Discovery)

Sublist3r automates subdomain discovery by aggregating data from multiple sources, significantly speeding up OSINT processes.

### Usage Example:

```bash
sublist3r -d domain.com
```

* `-d` specifies the target domain for subdomain enumeration.

**Sources used by Sublist3r:**

* Search Engines: Google, Bing, Yahoo
* Certificate Transparency Logs
* Various security databases

---

## Task 6: Virtual Hosts Enumeration (ffuf)

Virtual Hosts Enumeration identifies subdomains by altering the HTTP Host header. It is especially effective in discovering internal or staging subdomains that are not listed in public DNS.

### ⚙️ **Enumeration Steps Using ffuf:**

**Initial Enumeration Command:**

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://MACHINE_IP
```

* `-w`: Specifies the wordlist containing potential subdomains.
* `-H`: Modifies the HTTP Host header, inserting potential subdomains.
* `FUZZ`: Placeholder replaced with words from the wordlist.

**Filtering Results by Size (Removing False Positives):**

Run the command and note the common response size. Replace `{size}` with this number:

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt \
-H "Host: FUZZ.acmeitsupport.thm" \
-u http://MACHINE_IP -fs {size}
```

**Practical Example:**

```
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt \
-H "Host: FUZZ.acmeitsupport.thm" \
-u http://10.10.10.10 -fs 2395
```

---

### 📌 Recommended Best Practices:

* Perform subdomain enumeration regularly to maintain comprehensive asset inventories.
* Combine multiple enumeration methods (Brute Force, OSINT, Virtual Host) for thorough discovery.
* Always verify automated results manually to ensure accuracy and reliability.
* Continuously update wordlists and enumeration techniques to enhance discovery effectiveness.

