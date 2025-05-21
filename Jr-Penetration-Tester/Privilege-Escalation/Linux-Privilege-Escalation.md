# TryHackMe: Linux Privilege Escalation - Complete Summary (Task 1–12)

---

### 🔰 Task 1: Introduction

Privilege escalation in Linux systems is essential for CTFs, OSCP, and real-world penetration testing. Success depends on factors such as kernel version, installed applications, available programming languages, and user credentials. This room covers essential escalation vectors and techniques.

---

### 🔓 Task 2: What is Privilege Escalation?

![Privilege Escalation Diagram](https://github.com/user-attachments/assets/45e837d3-df6f-4f97-99c7-d13e9da4a317)

**Definition**: The process of moving from a lower-privileged account to a higher-privileged one (e.g., root).

**Importance**:
- Rare to gain root on first access.
- Escalation allows:
  - Password reset
  - File/system access bypass
  - Configuration changes
  - Persistence setup
  - Admin-level command execution

---

### 🧭 Task 3: Enumeration

![](https://github.com/user-attachments/assets/105bb8f6-332d-4314-9d4f-0196b4f60a11)
![](https://github.com/user-attachments/assets/15ce968a-ac8d-442b-bb72-197b70f04053)
![](https://github.com/user-attachments/assets/c633653b-00cf-44f8-a536-53e125f1c672)
![](https://github.com/user-attachments/assets/6ac85dc4-a451-4dba-a750-0b5c15109ea3)
![](https://github.com/user-attachments/assets/baaa995d-60c8-4234-b4ea-8632a4cf3673)
![](https://github.com/user-attachments/assets/224df8bf-c92b-422e-92c0-5e44ee48c0b9)
![](https://github.com/user-attachments/assets/a0569ecc-e875-4e9f-8ff6-bb2f07e5fac9)
![](https://github.com/user-attachments/assets/f98e313c-cb96-406b-b303-56cf87b48b1a)
![](https://github.com/user-attachments/assets/e4ad7d8c-4777-43d6-a61c-2ac4d0025542)
![](https://github.com/user-attachments/assets/26984367-64b5-4f08-aa41-5ba5a65ca0b0)
![](https://github.com/user-attachments/assets/dfed4aa3-de6d-429b-a138-a78a9e99b827)
![](https://github.com/user-attachments/assets/81c38ab5-1314-4615-9bbf-ce713db34f94)
![](https://github.com/user-attachments/assets/89ca12f2-970d-4b5c-ab57-c891e0d55b8b)
![](https://github.com/user-attachments/assets/b7af65f6-971d-45a9-b56f-d7b1e1545779)
![](https://github.com/user-attachments/assets/700f57d0-4197-4e28-95d6-08ef63844e86)
![](https://github.com/user-attachments/assets/b0dc65dc-611d-4637-96c9-6c1e4f786385)
![](https://github.com/user-attachments/assets/4374dbc0-3854-4a34-94cc-f78a4610e4bd)
![](https://github.com/user-attachments/assets/60dc6007-761d-4f9b-a0d5-13afd5821ddd)
![](https://github.com/user-attachments/assets/081e5c4d-662d-4caf-bb14-2530d0ab689b)
![](https://github.com/user-attachments/assets/1d80c956-c324-4e8f-a878-780a3442c06f)


Covers all foundational Linux commands to investigate the system:
- `ps`, `env`, `ls -la`, `id`, `whoami`, `/etc/passwd`, `history`
- `ifconfig`, `ip route`, `netstat`, `find`, `sudo -l`

Included screenshots:
- Process trees, user info, netstat output, hidden files, and find results.

---

### 🤖 Task 4: Automated Enumeration Tools

Recommended tools:
- LinPEAS
- LinEnum
- Linux Exploit Suggester (LES)
- Linux Smart Enumeration (LSE)
- Linux Priv Checker

---

### 💣 Task 5: Kernel Exploits

- Identify kernel: `uname -a`
- Find CVEs: ExploitDB, CVEDetails
- Compile & transfer exploits to target
- Risk of crash: use in test environments

---

### 🔐 Task 6: SUDO Misconfigurations

![Apache2 usage options](https://github.com/user-attachments/assets/e8b04c82-f55f-450f-8842-cf171e1d3397)
![sudo -l with LD_PRELOAD](https://github.com/user-attachments/assets/da9b0613-499f-4959-b731-bc55e60924ea)
![LD_PRELOAD compile](https://github.com/user-attachments/assets/c0d95599-603b-44a8-a62d-766854b1d7d1)
![LD_PRELOAD exploit result](https://github.com/user-attachments/assets/7d6c5585-a1c9-4d6c-8304-5b1f504b9fb2)

- Check `sudo -l`
- Use LD_PRELOAD or GTFOBins tricks
- Escalate via allowed binaries

---

### 🎯 Task 7: SUID Binaries

![find suid](https://github.com/user-attachments/assets/34b2af9c-817e-40fb-bd4c-14f1eec91d9f)
![GTFOBins reference](https://github.com/user-attachments/assets/239d2427-c9ee-433f-b3bc-40c0881ec97a)
![/etc/shadow read](https://github.com/user-attachments/assets/689b96ad-0cc3-4752-9b63-3bbb9e33962c)
![unshadow](https://github.com/user-attachments/assets/243680a3-58e0-4c54-8572-f5d28f7c109d)
![openssl hash](https://github.com/user-attachments/assets/5acd3108-11ad-4e04-b0e1-80839597bdb2)
![manual user insert](https://github.com/user-attachments/assets/d3c05bb8-a1ff-4e8e-a1dc-0e2d3abf5a63)
![root shell](https://github.com/user-attachments/assets/fa17ad87-a4ae-4e22-9597-8f51a314f742)

- Find files with `-perm -4000`
- Use GTFOBins to exploit
- Read `/etc/shadow` or inject root user

---

### ⚙️ Task 8: Capabilities

![getcap](https://github.com/user-attachments/assets/72f96d2a-cda0-4fcf-91cd-aace6252fb9a)
![vim binary](https://github.com/user-attachments/assets/376292c2-cd7d-4c36-a58b-8f0d9141ac81)
![exploit execution](https://github.com/user-attachments/assets/247d32c2-4752-47da-9af6-649d8fd090d1)
![id confirmation](https://github.com/user-attachments/assets/79f8b6b6-2d1c-4f7a-bd4e-9f83ae2056ab)

- Use `getcap -r /`
- Look for binaries with `cap_setuid+ep`
- Exploit via Python, vim, etc.

---

### ⏰ Task 9: Cron Jobs

![crontab](https://github.com/user-attachments/assets/dc081f7c-5022-4a74-a8c7-0aa17a4f791c)
![backup.sh](https://github.com/user-attachments/assets/d3b010f5-4f5e-4cc6-ba2b-7c0f0e92ddf2)
![shell inserted](https://github.com/user-attachments/assets/504a81ba-2718-4724-991a-2b1729411558)
![nc 6666](https://github.com/user-attachments/assets/86e79ec9-7d9c-482a-92f9-39723d667cd8)
![crontab orphan](https://github.com/user-attachments/assets/fb9e868e-6a3b-4df9-9816-296317e289ed)
![new payload](https://github.com/user-attachments/assets/4b81f30f-2dae-4b5a-8e23-059821c350c9)
![nc 7777](https://github.com/user-attachments/assets/63670660-eb38-4034-97f7-aeed09b8c9a9)

- Look in `/etc/crontab`
- Modify writable scripts
- Inject shell payloads

---

### 📁 Task 10: PATH Vulnerabilities

![echo path](<img width="477" alt="스크린샷 2025-05-20 오후 12 34 14" src="https://github.com/user-attachments/assets/997b030e-388e-4345-8f27-31f5c8288ebb" />
)
![path_exp.c](<img width="400" alt="스크린샷 2025-05-20 오후 12 34 20" src="https://github.com/user-attachments/assets/301d9e50-3bc2-4e62-8b61-a50010e841e9" />
)
![compiled binary](<img width="743" alt="스크린샷 2025-05-20 오후 12 34 27" src="https://github.com/user-attachments/assets/e10ec572-6d34-4708-b181-65e92e7f22a0" />
)
![ls view](<img width="612" alt="스크린샷 2025-05-20 오후 12 34 33" src="https://github.com/user-attachments/assets/9fd00388-e509-427a-9569-a779f8fb1a02" />
)
![writable dirs](<img width="475" alt="스크린샷 2025-05-20 오후 12 34 40" src="https://github.com/user-attachments/assets/fe45a955-a32c-4eed-b089-af3399aa2b52" />
)
![echo again](스크린샷 2025-05-20 오후 12.34.47)
![add tmp](<img width="931" alt="스크린샷 2025-05-20 오후 12 34 53" src="https://github.com/user-attachments/assets/1905c3c0-a643-4796-8e16-2f004ede7e4e" />
)
![fake binary](<img width="934" alt="스크린샷 2025-05-20 오후 12 35 02" src="https://github.com/user-attachments/assets/81da9405-3d52-4118-9962-bd7da8d6bdc1" />
)
![whoami](<img width="563" alt="스크린샷 2025-05-20 오후 12 35 09" src="https://github.com/user-attachments/assets/8dfdd993-98a6-42fb-a33a-cee2871d2aee" />
)
![root confirmed](<img width="934" alt="스크린샷 2025-05-20 오후 12 35 15" src="https://github.com/user-attachments/assets/179cedd0-20c8-42bc-be03-5dfd86af0de9" />
)

- Writable directories in $PATH can be hijacked
- Create fake binary with root SUID

---

### 🗂 Task 11: NFS Misconfigurations

![/etc/exports](./스크린샷_2025-05-20_오후_12.36.00.png)
![showmount](./스크린샷_2025-05-20_오후_12.36.05.png)
![mount nfs](./스크린샷_2025-05-20_오후_12.36.11.png)
![nfs.c](./스크린샷_2025-05-20_오후_12.36.18.png)
![compile suid](./스크린샷_2025-05-20_오후_12.36.24.png)
![execute root](./스크린샷_2025-05-20_오후_12.36.30.png)

- Misconfigured `no_root_squash`
- Upload SUID root shell via mount

---

### 🎓 Task 12: Capstone Challenge

You’ve completed all major Linux privilege escalation techniques. Now test them in a live environment.

**Target machine**
- Username: `leonard`
- Password: `Penny123`

**Goal**: Get root using:
- Kernel exploits
- SUID/SUDO tricks
- Cron jobs
- PATH hijack
- NFS misconfig

> “Privilege escalation is often more an art than a science.”
