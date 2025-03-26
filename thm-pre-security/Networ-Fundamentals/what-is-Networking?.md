# 🌐 TryHackMe - Network Fundamentals

> Learn the basics of networking: how devices communicate, identify themselves, and interact across the Internet.

---

## 🧠 Task 1: What is Networking?

Networking is simply about things being connected — whether people, systems, or devices.  
In computing, networks can be made of 2 to billions of devices, including phones, laptops, IoT, etc.

![Alice-Bob-Jim Network](https://github.com/user-attachments/assets/f9315173-f03f-47ff-a858-fd23fa8c3afe)

📌 Networking is essential in cybersecurity to understand how devices communicate and where vulnerabilities lie.

---

## 🌍 Task 2: What is the Internet?

The Internet is a giant network made up of many smaller private networks, all connected to form one global public network.

![Alice-Zayn-Toby](https://github.com/user-attachments/assets/25934755-f1e5-45ee-acf9-88e558e479f2)

Alice acts as a translator or connector between two groups that don’t share the same “language” — just like routers and gateways on the Internet.

![Multiple Networks Diagram](https://github.com/user-attachments/assets/a40e88c8-b1ab-41ac-96a6-82fb4233e36d)

📌 Public networks connect private ones — that’s what makes up the Internet.

---

## 📡 Task 3: Identifying Devices on a Network

Every device must have an identity on the network, just like people have names and fingerprints.

### 🧾 IP Address

IP addresses are temporary identifiers. They can be public or private.

![IP Octets Breakdown](https://github.com/user-attachments/assets/568ff589-86d6-4dcd-8987-2546a830c44f)

Example:

| Device Name     | IP Address     | Type    |
|------------------|----------------|---------|
| DESKTOP-KJE57FD | 192.168.1.77   | Private |
| CMNatic-PC      | 192.168.1.74   | Private |

![Private IP + MAC](https://github.com/user-attachments/assets/68fb2283-2a5f-4709-8c8a-ff8f01d468ca)


➡️ Both devices use their private IP to talk internally, and share a single public IP to talk to the Internet:

![Public IPv4](https://github.com/user-attachments/assets/e015d28d-f750-461c-a699-ccbe9de64b17)  
![IPv4 vs IPv6](https://github.com/user-attachments/assets/c8b61b1c-75af-4259-ad58-799bec81e384)

---

### 🔒 MAC Address

MAC addresses are like digital fingerprints — permanent and unique for each device.

![MAC Breakdown](https://github.com/user-attachments/assets/37e1e4ec-f85b-4d13-8db6-16f7db1c1ea2)

💡 MAC addresses can be **spoofed** — which is why relying solely on them for security can be dangerous (e.g., Wi-Fi access control at hotels).

---

## 📶 Task 4: Ping (ICMP)

`ping` is a network command used to check if a device is reachable and how fast the connection is.

```bash
ping 192.168.1.254
```
![IP 192.168.1.254](https://github.com/user-attachments/assets/a7e5d5be-eb2a-42bf-ad65-2e091e7ccffe)
