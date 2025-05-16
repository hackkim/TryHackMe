# 🚀 TryHackMe: Network Security - Nmap Post Port Scans

## 🔹 Task 1: Introduction

This is the **final room** in the Nmap series. Now that we've identified live systems and scanned their ports, it's time to move beyond simple enumeration.

We focus on the **post-scan phase**:
- Detect versions
- Detect OS
- Traceroute
- Scripting
- Exporting output

These help transition from **reconnaissance** to **vulnerability analysis**.

![Nmap Post-Scan Steps](https://github.com/user-attachments/assets/345d5273-07a7-46bf-9548-f27607ae645c)
*Post-scanning phases after identifying open ports*


## 🔹 Task 2: Service Detection

Use `-sV` to detect running service versions.

```bash
sudo nmap -sV MACHINE_IP
```

Control detection depth with:
- `--version-light` (level 2)
- `--version-all` (level 9)

Note:
- Requires full TCP connection (not stealth)
- Useful for vulnerability research

---

## 🔹 Task 3: OS Detection and Traceroute

### OS Detection

Use `-O` (uppercase o):

```bash
sudo nmap -sS -O MACHINE_IP
```

Nmap analyzes TCP/IP behavior to guess the OS. Accuracy depends on:
- Open and closed ports
- Virtualization impact
- OS fingerprint database

### Traceroute

Use `--traceroute`:

```bash
sudo nmap -sS --traceroute MACHINE_IP
```

Nmap traces hops **in reverse TTL** (from high to low), different from traditional `traceroute`.

---

## 🔹 Task 4: Nmap Scripting Engine (NSE)

Nmap includes hundreds of scripts written in **Lua**.

Script types:
- `default`, `auth`, `brute`, `vuln`, `safe`, `exploit`, `dos`, etc.

### Default scripts

```bash
sudo nmap -sS -sC MACHINE_IP
```

### Specific scripts

```bash
sudo nmap --script "http-date" MACHINE_IP
sudo nmap --script "ftp*" MACHINE_IP
```

📁 NSE scripts directory:
```
/usr/share/nmap/scripts
```

Be cautious with intrusive or exploitative scripts.

---

## 🔹 Task 5: Saving the Output

### Normal format

```bash
nmap -oN scan.txt MACHINE_IP
```

- Human-readable
- Similar to screen output

### Grepable format

```bash
nmap -oG scan.gnmap MACHINE_IP
```

- Machine-parseable
- Each line is independent

### XML format

```bash
nmap -oX scan.xml MACHINE_IP
```

- Great for programmatic parsing

### All formats

```bash
nmap -oA scan MACHINE_IP
```

- Generates `.nmap`, `.gnmap`, and `.xml`

### Script Kiddie output (for fun)

```bash
nmap -oS scan.kiddie MACHINE_IP
```

---

## 🔹 Task 6: Summary

| Option                      | Purpose                                       |
|-----------------------------|-----------------------------------------------|
| `-sV`                      | Service/version detection                     |
| `--version-light`          | Light detection (level 2)                     |
| `--version-all`            | Full detection (level 9)                      |
| `-O`                       | OS detection                                  |
| `--traceroute`             | Run traceroute                                |
| `--script=SCRIPT_NAME`     | Run selected NSE script(s)                    |
| `-sC` or `--script=default`| Run default scripts                           |
| `-A`                       | Equivalent to `-sV -O -sC --traceroute`       |
| `-oN`                      | Normal format output                          |
| `-oG`                      | Grepable format output                        |
| `-oX`                      | XML format output                             |
| `-oA`                      | Save all formats                              |

---

✅ With service versions, OS guesses, and scripts, you now know how to use Nmap not just to scan, but to **enumerate** and **document** critical target details. Time to move on to vulnerability analysis!
