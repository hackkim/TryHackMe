# 🔍 TryHackMe: Nmap Basic Port Scans

This room, the second in the Nmap series, focuses on identifying **open TCP and UDP ports** using Nmap. It expands on basic scan types and explains the TCP/UDP behavior, scan modes, and performance tuning.

---

## 🔹 Task 1: Introduction

Following live host discovery, this room focuses on port scanning:

1. TCP Connect Scan (`-sT`)
2. TCP SYN Scan (`-sS`)
3. UDP Scan (`-sU`)

![Nmap Scan Flow](https://github.com/user-attachments/assets/13598158-c25a-4851-b994-5133d58d6237)
*Nmap scanning steps — current focus on port scanning*

---

## 🔹 Task 2: TCP and UDP Ports

Ports identify services on a host.

| State            | Description |
|------------------|-------------|
| Open             | Service is listening |
| Closed           | No service on port, port accessible |
| Filtered         | Firewalled, inaccessible |
| Unfiltered       | Accessible but state unknown |
| Open|Filtered    | Nmap can’t tell if open or filtered |
| Closed|Filtered  | Nmap can’t tell if closed or filtered |

---

## 🔹 Task 3: TCP Flags

Nmap relies on TCP headers for scanning.

![TCP Header (RFC793)](https://github.com/user-attachments/assets/02f33503-f8b0-49d6-9faf-6883de122134)
*TCP header structure — highlighting flag bits used by Nmap*

Flags used:
- `SYN` (synchronize)
- `ACK` (acknowledge)
- `RST` (reset)
- `FIN` (finish)
- `URG`, `PSH`

---

## 🔹 Task 4: TCP Connect Scan (`-sT`)

- Full **3-way handshake**
- Required for unprivileged users
- Likely to be logged on the target

```bash
nmap -sT MACHINE_IP
```

![TCP 3-Way Handshake](https://github.com/user-attachments/assets/66dd1905-c91f-4301-9dc4-8d592092a515)

![Nmap -sT Flow](https://github.com/user-attachments/assets/57c16408-1fa8-4fe9-ac30-e6ec02a5263a)

![Wireshark -sT All Ports](https://github.com/user-attachments/assets/05bff366-db5f-4b7b-bcb9-03633124a2a0)

![Wireshark -sT Port 143](https://github.com/user-attachments/assets/c0061632-3ea0-4925-a6a3-dd25dbc5da26)

---

## 🔹 Task 5: TCP SYN Scan (`-sS`)

- Default for **root/sudo** users
- Sends SYN → receives SYN/ACK → sends RST
- Stealthier than full handshake

```bash
sudo nmap -sS MACHINE_IP
```

![SYN Scan Flow](https://github.com/user-attachments/assets/c5925905-5128-46cc-9592-afa14151770e)

![Wireshark - TCP SYN Scan](https://github.com/user-attachments/assets/1f1a5b8f-804a-45bb-9bef-30be95df8df1)

![Wireshark - Connect vs SYN](https://github.com/user-attachments/assets/89f1a10e-1c5f-4cad-84d0-47950dfcf907)

---

## 🔹 Task 6: UDP Scan (`-sU`)

- Connectionless, no handshake
- Open ports give **no response**
- Closed ports respond with **ICMP Type 3 Code 3**

```bash
sudo nmap -sU MACHINE_IP
```

![UDP Open - No Response](https://github.com/user-attachments/assets/f2ffffe5-c250-4e24-84b9-f0536b6919b9)

![UDP Closed - ICMP Response](https://github.com/user-attachments/assets/b1d9231b-3e6e-49a5-b725-36cf4f148b9e)

![Wireshark - UDP Scan ICMP Responses](https://github.com/user-attachments/assets/3be4b2c8-50cb-4c53-a49e-2000ad2d50c6)

---

## 🔹 Task 7: Fine-Tuning Scope and Performance

### Port Scope
```bash
-p22,80,443      # specific ports
-p1-1023         # common privileged ports
-p-              # all 65535 ports
-F               # top 100 common ports
--top-ports 10   # top 10 most common ports
```

### Scan Timing
```bash
-T0 to -T5
--min-rate 10
--max-rate 100
--min-parallelism 100
--max-parallelism 500
```

| Template  | Behavior   |
|-----------|------------|
| T0        | Paranoid (slowest) |
| T1        | Sneaky     |
| T2        | Polite     |
| T3        | Normal     |
| T4        | Aggressive |
| T5        | Insane     |

---

## 🔹 Task 8: Summary

| Scan Type       | Command                    |
|------------------|-----------------------------|
| TCP Connect      | `nmap -sT MACHINE_IP`       |
| TCP SYN          | `sudo nmap -sS MACHINE_IP`  |
| UDP Scan         | `sudo nmap -sU MACHINE_IP`  |

| Option                | Purpose                                |
|------------------------|----------------------------------------|
| `-p-`                 | Scan all ports                         |
| `-p1-1023`            | Common ports                           |
| `-F`                 | Fast (top 100)                          |
| `-r`                 | Scan in order                          |
| `-T0` to `-T5`        | Timing templates                       |
| `--max-rate 50`      | Limit rate                             |
| `--min-parallelism`  | Ensure minimum parallel probes         |

---

✅ You’ve now learned how to discover open TCP and UDP services using Nmap. This foundational skill prepares you for deeper enumeration, version detection, and vulnerability scanning.
