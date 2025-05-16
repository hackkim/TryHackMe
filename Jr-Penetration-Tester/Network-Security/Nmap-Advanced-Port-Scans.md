# 🎯 TryHackMe: Nmap Advanced Port Scans

This room introduces advanced scanning techniques using TCP flag manipulation, spoofing, packet fragmentation, and stealth strategies. These methods can be used to bypass firewalls, avoid detection, and conduct in-depth network reconnaissance.

---

## 🔹 Task 1: Introduction

This is the third room in the Nmap series.

Covered previously:
1. Enumerate targets
2. Discover live hosts
3. Reverse-DNS lookup
4. ✅ Scan ports (now with advanced methods)

Focus in this room:
- Null, FIN, Xmas, Maimon, ACK, Window, Custom Flag scans
- IP/MAC spoofing, Decoys
- Fragmented packets, Idle/Zombie scans

![TCP Header (RFC793)](https://github.com/user-attachments/assets/7b2c7292-e01c-41ba-811d-48f8047b263c)

---

## 🔹 Task 2: TCP Null, FIN, and Xmas Scans

### Null Scan (`-sN`)

- No TCP flags are set
- Closed ports reply with RST
- Open or filtered ports = no response

```bash
sudo nmap -sN MACHINE_IP
```

![Null Open](https://github.com/user-attachments/assets/f1b27be2-6e6e-4ce1-9d3f-1d02d40141c4)
![Null Closed](https://github.com/user-attachments/assets/571fa12c-87f8-48f9-99a6-707c8a0ca985)

---

### FIN Scan (`-sF`)

- Sends only FIN flag
- Same logic as null scan

```bash
sudo nmap -sF MACHINE_IP
```

![FIN Open](https://github.com/user-attachments/assets/0693464e-84d2-4f88-a8ed-bd3200e1c4b2)
![FIN Closed](https://github.com/user-attachments/assets/360a46ce-404e-4725-8db3-8dcebc693c91)

---

### Xmas Scan (`-sX`)

- Sends FIN, PSH, and URG
- Named like a "Christmas tree"

```bash
sudo nmap -sX MACHINE_IP
```

![Xmas Scan Logic](https://github.com/user-attachments/assets/8caee9cb-5d06-48bc-941f-812cf3960d1d)

---

## 🔹 Task 3: TCP Maimon Scan

- Sends FIN + ACK
- Designed to confuse BSD-based stacks
- Rarely effective today

```bash
sudo nmap -sM MACHINE_IP
```

![Maimon Scan Logic](https://github.com/user-attachments/assets/2c48b3f9-6a64-44fa-a2d3-3fcaa7ae5b43)

---

## 🔹 Task 4: ACK, Window, and Custom Scans

### ACK Scan (`-sA`)

- Sends ACK
- Firewall detection (not port state)

```bash
sudo nmap -sA MACHINE_IP
```

![ACK Scan Flow](https://github.com/user-attachments/assets/5af27732-9e4f-47de-bbe4-4529602b148e)

---

### Window Scan (`-sW`)

- Uses ACK behavior
- Reads window size to infer port state

```bash
sudo nmap -sW MACHINE_IP
```

![Window Scan Logic](https://github.com/user-attachments/assets/388b0460-6d9d-470e-8add-dcbdb43b6c6c)

---

### Custom Scan (`--scanflags`)

```bash
sudo nmap --scanflags URGACKPSHRSTSYNFIN MACHINE_IP
```

![Custom Scan Flag Flow](https://github.com/user-attachments/assets/e608deb6-5def-49aa-b452-fbdcadcdad4a)

---

## 🔹 Task 5: Spoofing and Decoys

### IP Spoofing

```bash
sudo nmap -e eth0 -Pn -S SPOOFED_IP MACHINE_IP
```

![IP Spoofing Flow](https://github.com/user-attachments/assets/0782a1c7-efec-4d10-ac66-c83162cedd2b)

---

### Decoy Scan

```bash
nmap -D 10.10.0.1,10.10.0.2,ME MACHINE_IP
```

![Decoy Scan Logic](https://github.com/user-attachments/assets/080caa35-8765-4660-a0aa-e0fec2b34b1f)

---

## 🔹 Task 6: Fragmented Packets

- Breaks TCP/IP packets into 8-byte or 16-byte fragments
- Used to evade signature-based firewalls/IDS

```bash
sudo nmap -sS -p80 -f MACHINE_IP
```

![IP Header (RFC 791)](https://github.com/user-attachments/assets/4b61aa24-11e0-44de-adf8-91aa75705b34)

Without Fragmentation:
![Normal TCP Packet](https://github.com/user-attachments/assets/564117f1-a03d-4844-aa8a-a04e10cb93d0)

With Fragmentation:
![Fragmented TCP Packets](https://github.com/user-attachments/assets/44434610-23c4-443d-8a07-a49991c789a1)

---

## 🔹 Task 7: Idle (Zombie) Scan

- Uses a quiet third-party system to stealthily probe target

```bash
sudo nmap -sI ZOMBIE_IP MACHINE_IP
```

Step 1: Check Zombie IP ID  
![Idle Scan Step 1](https://github.com/user-attachments/assets/2eabbbc9-be87-43a7-983b-45dcf654c304)

Step 2: SYN → Target (spoofed from Zombie)  
**Port Closed**:  
![Idle Scan - Closed](https://github.com/user-attachments/assets/857eeea2-95aa-4d9e-90f1-6e845cb91b2c)  
**Port Open**:  
![Idle Scan - Open](https://github.com/user-attachments/assets/a50efc11-224b-4349-b0f7-a955a8e7524c)

---

## 🔹 Task 8: Getting More Details

### Add Reasoning
```bash
sudo nmap -sS --reason MACHINE_IP
```

### Verbose Output
```bash
-v, -vv, -d, -dd
```

Used for:
- Debugging
- Understanding scan logic
- Generating more detailed reports

---

## 🔹 Task 9: Summary

| Scan Type        | Command Example                                  |
|------------------|---------------------------------------------------|
| Null Scan        | `sudo nmap -sN MACHINE_IP`                        |
| FIN Scan         | `sudo nmap -sF MACHINE_IP`                        |
| Xmas Scan        | `sudo nmap -sX MACHINE_IP`                        |
| Maimon Scan      | `sudo nmap -sM MACHINE_IP`                        |
| ACK Scan         | `sudo nmap -sA MACHINE_IP`                        |
| Window Scan      | `sudo nmap -sW MACHINE_IP`                        |
| Custom Flags     | `sudo nmap --scanflags URGACKPSHRSTSYNFIN ...`   |
| IP Spoofing      | `sudo nmap -S SPOOFED_IP MACHINE_IP`             |
| MAC Spoofing     | `--spoof-mac SPOOFED_MAC`                         |
| Decoy Scan       | `nmap -D 10.10.0.1,10.10.0.2,ME MACHINE_IP`       |
| Idle Scan        | `sudo nmap -sI ZOMBIE_IP MACHINE_IP`             |
| Fragmentation    | `sudo nmap -sS -p80 -f MACHINE_IP`               |

| Option            | Purpose                                  |
|-------------------|-------------------------------------------|
| `--reason`        | Show why Nmap reached its conclusions     |
| `-v`, `-vv`       | Verbose/very verbose                      |
| `-d`, `-dd`       | Debug/debug++                             |
| `--data-length`   | Pad packets with additional bytes         |

---

✅ You now understand stealthy and evasive scan techniques, critical for penetration testing and red teaming in hardened environments.
