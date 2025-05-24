# TryHackMe - Windows Privilege Escalation

## 🔰 Task 1: Introduction: Introduction
Unprivileged users have limited access. The goal of this room is to explore techniques to escalate privileges to an Administrator or SYSTEM user.

## 🧭 Task 2: Windows Privilege Escalation Concepts: Windows Privilege Escalation Concepts

- **Privilege Escalation**: Gaining access from a lower privilege (e.g., user A) to a higher one (e.g., user B).
- **Common Vectors**:
  - Misconfigured services or scheduled tasks
  - Excessive privileges
  - Vulnerable software
  - Missing patches

### Windows User Types
- **Administrators**: Full system control.
- **Users**: Limited access.
- **SYSTEM**: OS internal tasks, higher than admin.
- **Local Service / Network Service**: Minimal privileges for services.

## 🔍 Task 3: Harvesting Passwords from Common Locations: Harvesting Passwords

- **Unattended Installations**: Look for credentials in:
  - `C:\Unattend.xml`
  - `C:\Windows\Panther\Unattend.xml`
  - ...
- **PowerShell History**: Look in `%userprofile%\AppData\...\ConsoleHost_history.txt`
- **Saved Credentials**: `cmdkey /list`, `runas /savecred`
- **IIS Configs**: Look in `web.config` for DB credentials.
- **PuTTY**: Registry lookup:
  - `reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s`

## ⚡ Task 4: Other Quick Wins: Other Quick Wins

- **Scheduled Tasks**: Check with `schtasks` and permission via `icacls`.
- **AlwaysInstallElevated**: Exploit with malicious `.msi` if registry keys are set.

## 🛠 Task 5: Abusing Service Misconfigurations: Abusing Service Misconfigurations

![AppHostSvc Permissions](https://github.com/user-attachments/assets/8f08adec-a31a-4804-98a1-5b0cb6d46022)
*Service DACL for AppHostSvc showing Administrator-level control.*

![Registry Entry for AppHostSvc](https://github.com/user-attachments/assets/655f8f30-2fa4-43f8-9839-0f4162b02064)
*Registry configuration for AppHostSvc service path and privileges.*


- **Insecure Executable Permissions**:
  - Replace `.exe` with reverse shell.
- **Unquoted Paths**:
  - Hijack services looking for `C:\MyPrograms\Disk.exe`.
- **Service DACLs**:
  - Check with `accesschk` (e.g., `accesschk64.exe -qlc servicename`).
  - Modify service config via `sc config`.

## 🔐 Task 6: Abusing Dangerous Privileges: Abusing Dangerous Privileges

### Running Command Prompt with Elevated Privileges
![Run as Administrator](https://github.com/user-attachments/assets/386055a2-a9cc-4085-aa7b-d2bccbfc44bb)

### SeTakeOwnership Exploit – Lock Screen Access
![Lock the screen](https://github.com/user-attachments/assets/0d80fd48-0fb3-4c7c-a128-5a045736577c)
![Ease of Access - Utilman Bypass](https://github.com/user-attachments/assets/e0001fe9-738c-4f4c-8d87-8f1e223afe20)
![SYSTEM Shell via Utilman](https://github.com/user-attachments/assets/f391d031-8596-4e29-9a6a-a2d6839a52b5)

### SeImpersonate / SeAssignPrimaryToken – Token Hijacking
![Token usage without impersonation](https://github.com/user-attachments/assets/fa05d316-126a-4fc0-bdd5-41f352f59307)
![Token usage with impersonation](https://github.com/user-attachments/assets/ee4f6a0c-9953-4f17-ab95-68ebaffebac5)

### Checking Privileges
![whoami /priv output](https://github.com/user-attachments/assets/a30f2251-791e-4ce1-b8d7-dfec87674acc)

### Exploit in Action – RogueWinRM
![RogueWinRM Exploit](https://github.com/user-attachments/assets/1f4e6159-dbba-4fc2-85e3-dd850ecec6f5)


- **SeBackup / SeRestore**:
  - Use to copy `SAM` and `SYSTEM` registry hives.
  - Dump hashes with `secretsdump.py`.
- **SeTakeOwnership**:
  - Take ownership of `utilman.exe`, replace with `cmd.exe`, trigger from lock screen.
- **SeImpersonate / SeAssignPrimaryToken**:
  - Use `RogueWinRM` to impersonate SYSTEM via port 5985.

## 💥 Task 7: Abusing Vulnerable Software: Abusing Vulnerable Software

### Druva inSync RPC Exploit Packet Structure
![Druva inSync RPC Protocol](https://github.com/user-attachments/assets/22394534-3f6e-4e78-a192-925193b6833a)

### Running Elevated Command Prompt
![Run CMD as Admin](https://github.com/user-attachments/assets/8c609fac-71f8-4792-a4da-0254fab67f12)


- **Druva inSync 6.6.3**:
  - RPC port 6064, use path traversal in RPC call to run commands as SYSTEM.

## 🧰 Task 8: Tools of the Trade: Tools of the Trade

- **WinPEAS**: Comprehensive PE scanner.
- **PrivescCheck**: PowerShell-based privilege checker.
- **WES-NG**: Runs on attack box, uses `systeminfo.txt`.
- **Metasploit**: Use `multi/recon/local_exploit_suggester`.

## ✅ Task 9: Conclusion: Conclusion

Covered methods:
- Harvesting passwords
- Service misconfigs
- Dangerous privileges
- Vulnerable software
- Tools like WinPEAS, PrivescCheck, and WES-NG

### Further Resources
- PayloadsAllTheThings
- Priv2Admin
- Hacktricks
- Decoder’s Blog

Happy hacking!

