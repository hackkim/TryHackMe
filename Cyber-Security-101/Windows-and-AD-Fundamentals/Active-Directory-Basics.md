## 🪟 TryHackMe - Active Directory Basics

> A hands-on introduction to Active Directory (AD) — the backbone of Windows enterprise environments.  
> Learn how domains, users, groups, and permissions work inside a real-world Windows domain setup.

---

## 📘 Task 1 - Introduction

Microsoft's Active Directory (AD) simplifies management of devices and users in a corporate network.

### 🎯 Objectives
- Understand what Active Directory is
- Learn about AD Domains and Domain Controllers
- Explore core components of AD: users, computers, groups
- Visualize forests, trees, and trust relationships

### 🧠 Prerequisites
- Basic familiarity with Windows OS  
  (📝 [See: Windows Fundamentals module])

---

## 🏢 Task 2 - Windows Domains

Managing 5 employees manually is fine. But what if you have 157 computers and 320 users across 4 offices?  
You need centralized control. That’s where **Windows Domains** and **Active Directory** come in.

### 🧩 What is a Windows Domain?

- A **Windows Domain** is a group of computers and users managed centrally.
- AD stores all configuration and credentials.
- The server running AD is called a **Domain Controller (DC)**.

📌 Example Network Domain  
![AD Network Domain](https://github.com/user-attachments/assets/80f70bec-91c0-47ea-a385-2efa649a56f7)

---

### ✅ Benefits of AD

- **Centralized identity management**
- **Policy enforcement** (security, permissions, logon settings)

📌 RDP Login Info  
![Credentials](https://github.com/user-attachments/assets/17f4545d-1354-43ca-a680-c7c0b9144289)

Use `THM\Administrator` to log in via RDP.

---

## 📂 Task 3 - Active Directory Overview

Active Directory organizes and stores information about **all objects** in a domain.  
These include: users, computers, groups, printers, and more.

---

### 👤 AD Objects: Users

Users are **security principals** (can log in, be assigned permissions).  
Users can be:
- Real people (e.g., employees)
- Services (e.g., IIS, MSSQL run under special service accounts)

---

### 🖥️ AD Objects: Computers

- When a machine joins a domain, an account is created for it.
- Machines are **security principals** just like users.
- Format: `COMPUTERNAME$`

---

### 👥 AD Objects: Groups

Groups are used to assign permissions across many users or machines.

📌 Common Built-in Groups

| Group              | Description                                                        |
|-------------------|--------------------------------------------------------------------|
| Domain Admins      | Full control over the domain                                       |
| Server Operators   | Can manage DCs, but not change groups                              |
| Backup Operators   | Can read any file (backup role)                                    |
| Account Operators  | Can create/modify user accounts                                    |
| Domain Users       | All standard user accounts                                         |
| Domain Computers   | All computer accounts                                              |
| Domain Controllers | All DCs in the domain                                              |

---

### 🧭 Using "Active Directory Users and Computers"

This is the primary tool for managing AD users, groups, and OUs.

📌 Launch from Start Menu  
![Search ADUC](https://github.com/user-attachments/assets/3704081a-7dd2-4e3d-8279-adeddf9f248b)

---

### 🗂️ Organizational Units (OUs)

OUs are containers that help organize AD objects logically.

- OUs are used to apply **Group Policies**
- A user can belong to **only one OU** at a time
- Users can belong to **multiple groups**

📌 OU Hierarchy Example  
![OU Hierarchy](https://github.com/user-attachments/assets/cd2ea009-38de-4d95-adcb-f6a7d5fcc39a)

📌 Sample Users under IT OU  
![OU Users](https://github.com/user-attachments/assets/a5d071a4-4cfc-4dd6-8e0f-4db79b6c67ee)

---

### ⚖️ OUs vs. Groups

| Concept          | Purpose                              | Notes                                         |
|------------------|--------------------------------------|-----------------------------------------------|
| Organizational Unit (OU) | Apply GPOs / structure org         | 1 OU per user                                 |
| Security Group   | Assign permissions to resources      | Multiple groups per user allowed              |

OUs structure the domain — Groups control access.

---
## 👥 Task 4 - Managing Users in AD

Our first job as domain administrators is to review the Active Directory users and OUs and ensure they match the organizational structure.

---

### 🧱 Organizational Chart

📌 THM Inc. Departmental Overview  
![Org Chart]("https://github.com/user-attachments/assets/4f74d03d-17d7-40ea-a5f9-404c25a413c8)

---

### 🗑️ Deleting Extra OUs

We found an extra OU that doesn't appear in the chart. Trying to delete it prompts an error:

📌 Deletion Protection Error  
![OU Delete Error](https://github.com/user-attachments/assets/a7b07285-36be-4966-9d22-efa0fb9f10a8)

To resolve this:

1. Go to **View** > Enable **Advanced Features**  
   ![Advanced Features](https://github.com/user-attachments/assets/ee6e34bc-b1c6-498d-96fe-97d8ea13ad69)

2. Right-click the OU → **Properties** → **Object**  
3. Uncheck **Protect object from accidental deletion**  
   ![OU Protection](https://github.com/user-attachments/assets/94f5e913-8962-4265-b707-21cdeb01f04b)

You can now delete the OU and any users/groups under it.

---

### 🔁 Updating Users to Match the Chart

After deleting the extra OU, match the users to the chart by removing or creating as needed.

---

### 👨‍🔧 Delegating Password Reset Rights

We want to allow **Phillip (IT Support)** to reset passwords for users in Sales, Marketing, and Management.

1. Right-click the **Sales OU** → Select **Delegate Control**  
   ![Delegate Control](https://github.com/user-attachments/assets/9d11ebfc-3f89-4fcc-bf84-9233d40bbc8b)

2. Add **phillip** as the delegate  
   ![Delegate Add User](https://github.com/user-attachments/assets/9d88e02b-0d0d-4b60-91d2-b0b183b588a4)

3. Choose "Reset user passwords and force password change at next logon"  
   ![Delegate Reset Password](https://github.com/user-attachments/assets/99625136-768d-4514-b85a-c0753c322454)

---

### 🔑 Credentials to Use for Testing

Phillip's login credentials for RDP:

📌 Phillip's RDP Info  
![Phillip RDP](https://github.com/user-attachments/assets/697bf436-5bb6-4233-83be-625926c3dee8)

As Phillip, use PowerShell:

```powershell
Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose
```
```powershell
PS C:\Users\phillip> Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose

VERBOSE: Performing the operation "Set" on target "CN=Sophie,OU=Sales,OU=THM,DC=thm,DC=local".
```
---

## 🖥️ Task 5 - Managing Computers in AD

As a Domain Administrator, it's important to organize machines efficiently within the Active Directory (AD) to apply proper policies.  
By default, all newly joined machines are placed in the **Computers** container.

---

### 🗂️ Default View of Computers

When a domain is configured, all domain-joined machines are placed here initially:

![Default Computers Container](https://github.com/user-attachments/assets/a42ead85-2c26-4caa-a113-90958a025689)

In the above example, we see various machine accounts:
- Laptops: `LPT-*`
- Desktops: `PC-*`
- Servers: `SRV-*`, `SVR-*`

---

### 📁 Creating OUs for Workstations & Servers

To manage policies more efficiently, we create **Organizational Units (OUs)** that separate **Workstations** and **Servers**.

📌 Newly created OU structure:
- `Workstations` → for employee laptops/desktops
- `Servers` → for back-end or infrastructure systems

![Created OUs](https://github.com/user-attachments/assets/4cdbccf9-755d-40db-92a8-effc93acd804)

---

### ✅ What You Should Do

1. **Create OUs**: Right-click on the domain root (`thm.local`) and create OUs:  
   - `Workstations`  
   - `Servers`

2. **Move Machines**: Drag and drop computers into the appropriate OU:
   - `LPT-*`, `PC-*` → Workstations  
   - `SRV-*`, `SVR-*` → Servers

3. **Benefits**:  
   - Better control over GPO (Group Policy Objects)  
   - Easier to deploy configurations or security baselines  

---

> 💡 Pro Tip: Once the machines are categorized, you can link GPOs to each OU to enforce policies like screen lock timers, software installations, or restricted access to system settings.


## 🛠️ Task 6 - Group Policies

Group Policies allow administrators to manage configurations for users and computers across the domain using Group Policy Objects (GPOs). These are essential for enforcing security settings, software installations, and user restrictions.

---

### 📌 Accessing the Group Policy Management Console

To get started, launch **Group Policy Management** from the Start menu.

![Group Policy Management](https://github.com/user-attachments/assets/37ad00e6-2131-4e48-b1c4-f2ab9da21c18)

---

### 🧱 Creating and Linking GPOs

GPOs are created under **Group Policy Objects** and then linked to Organizational Units (OUs) to take effect.

![GPOs created and linked](https://github.com/user-attachments/assets/94b345c9-6a24-4837-9098-09b6551872cb)

---

### 🔎 Viewing GPO Scope

Each GPO has a **Scope** tab that shows where the policy is linked and who it applies to.

![Scope tab](https://github.com/user-attachments/assets/86985c76-e3dc-47b6-ac39-af26d0fac116)

---

### ⚙️ Viewing GPO Settings

The **Settings** tab shows which policies are active under Computer or User Configuration.

![GPO Settings tab](https://github.com/user-attachments/assets/f22fcc82-3069-4a42-94d0-5672d6263dbd)

---

### 🔐 Default Domain Policy Example

The **Default Domain Policy** typically includes password policies and lockout settings.

![Default domain policy details](https://github.com/user-attachments/assets/8e428c99-fc13-42c5-b15f-7d42bca0f358)

---

### ✏️ Editing GPOs

To modify a GPO, right-click and choose **Edit**.

![Edit GPO](https://github.com/user-attachments/assets/06a91c97-df20-45f1-b12f-dc88e76ebe8d)

---

### 🔏 Enforcing Password Complexity

Navigate to the password policy settings and adjust options like **minimum password length**.

![Minimum password length](https://github.com/user-attachments/assets/d1044ace-acf0-4e2b-9cec-350937213f1a)

---

### ❓ Learn More via 'Explain' Tab

Use the **Explain** tab to read detailed descriptions of each setting.

![Explain tab](https://github.com/user-attachments/assets/20d9e950-65fe-400e-a2dd-96046dfddff6)

---

## 🎯 Restrict Control Panel Access

Create a new GPO and enable the setting:

**User Configuration → Admin Templates → Control Panel → Prohibit access to Control Panel and PC settings**

![Prohibit Control Panel Access](https://github.com/user-attachments/assets/1c784e04-e96b-4775-ac96-a90744e264f3)

---

### 🔗 Link GPO to Targeted OUs

Apply this GPO only to OUs that require restrictions (e.g., Sales, Management).

![Linking Control Panel GPO](https://github.com/user-attachments/assets/dc00c45e-a2c4-4eac-af24-6c8d3d741909)

---

## 🖥️ Auto Lock Screen GPO

Create a GPO to automatically lock the screen after inactivity.

**Computer Configuration → Policies → Windows Settings → Security Settings → Local Policies → Security Options → Interactive logon: Machine inactivity limit**

Set to **300 seconds (5 minutes)**.

![Auto Lock Screen setting](<img width="795" alt="스크린샷 2025-04-06 오후 11 18 05" src="https://github.com/user-attachments/assets/80c3258e-71d2-4977-8241-7dfb30ed6cd6" />
)

---

### 🔗 Linking Auto Lock Screen GPO

Link the Auto Lock Screen policy to the domain so it affects all workstations.

![Auto Lock Screen GPO linked](<img width="929" alt="스크린샷 2025-04-06 오후 11 18 11" src="https://github.com/user-attachments/assets/966a7518-d204-4283-b3ff-6e4838653d9f" />
)

---

### 🔐 Testing as a User

Login using a test user (e.g., Mark) to confirm that restrictions and lockouts are working properly.

![Mark credentials](https://github.com/user-attachments/assets/11d7383f-00d9-4003-aeb9-99bd6774c712)

---

## 🔐 Task 7 - Authentication Methods

When using Windows domains, user credentials are centrally stored on **Domain Controllers**. Whenever a domain user attempts to authenticate to a service, the request is verified through the DC using one of two authentication protocols:

- **Kerberos** (default in modern Windows domains)
- **NetNTLM** (legacy, kept for compatibility)

---

### 🧾 Kerberos Authentication

Kerberos is a ticket-based protocol that uses session keys and a ticket-granting mechanism to enable secure authentication.

---

### 🎟️ 1. Requesting a Ticket Granting Ticket (TGT)

The client sends its **username** and an encrypted **timestamp** to the Key Distribution Center (KDC).

📌  
![Kerberos Step 1 - Request TGT](https://github.com/user-attachments/assets/cf5c1317-f767-4e82-8d59-296a63fcd145)

The KDC replies with:

- A **TGT** (Ticket Granting Ticket), encrypted using the krbtgt account hash
- A **session key** for the client

---

### 🎫 2. Requesting a Service Ticket (TGS)

To access a service (e.g., MSSQL), the client uses the TGT to request a **TGS** (Ticket Granting Service) from the KDC, including:

- The **TGT**
- An encrypted timestamp using the session key
- The **SPN** (Service Principal Name)

📌  
![Kerberos Step 2 - Request TGS](https://github.com/user-attachments/assets/c0b482c9-6623-47c4-b41f-528273dc6438)

The KDC responds with:

- A **TGS** for the service, encrypted with the service owner's password hash
- A **service session key**

---

### 🖥️ 3. Authenticating to the Service

The client sends the **TGS** and an encrypted **timestamp** to the target service to prove identity.

📌  
![Kerberos Step 3 - Authenticate to Service](https://github.com/user-attachments/assets/f68b1cbd-3de4-4ed7-85da-58af8382147b)

---

### 🧱 NetNTLM Authentication

NetNTLM is a legacy challenge-response authentication protocol. While outdated, it's still supported in many networks for compatibility.

---

### 🔁 NetNTLM Flow

1. Client sends an authentication request to the server.
2. Server issues a **random challenge**.
3. Client combines its **NTLM hash** with the challenge and replies with a **response**.
4. Server forwards the challenge and response to the DC.
5. The DC calculates the expected response using the stored hash and compares.
6. Authentication is either allowed or denied.

📌  
![image](https://github.com/user-attachments/assets/465ca03b-6df1-425a-8fd2-9737121f7456)

> ⚠️ Password hashes are never sent across the network in plain text.

---
## 🌳 Task 8 - Trees, Forests, and Trusts

In large enterprise environments, a single domain might not be sufficient. Microsoft’s Active Directory allows organizing domains into trees and forests and managing trust relationships between them.

---

### 🏢 Single Domain Structure

A basic domain structure consists of a domain controller and other systems (file server, workstation, etc.) under one namespace.

![Domain Structure](https://github.com/user-attachments/assets/4b718bca-5a75-4e5f-a64d-ebb922ab1f65)

---

### 🌲 Domain Trees

A tree is a collection of domains that share a contiguous namespace. For example:

- Root domain: `thm.local`
- Child domains: `uk.thm.local`, `us.thm.local`

Each domain can be administered independently, but they’re part of the same tree.

![Tree Structure](https://github.com/user-attachments/assets/70613072-a20f-4dfe-8255-b82c0bb1814a)

---

### 🌳 Forests

A forest is a collection of trees that do not necessarily share the same namespace. Each tree in the forest can contain multiple domains.

Example:
- `thm.local` tree (with `uk.thm.local`, `us.thm.local`)
- `mht.local` tree (with `eu.mht.local`, `asia.mht.local`)

Together they form a forest.

![Forest Structure](https://github.com/user-attachments/assets/98bc2206-911c-462e-b472-43a52ae66f8d)

---

### 🔐 Trust Relationships

Trusts allow users in one domain to access resources in another domain.

- 🔄 Two-way trust: Both domains trust each other.
- 🔁 One-way trust: Only one domain trusts the other.

For example:
If `Domain AAA` trusts `Domain BBB`, users in `BBB` can access resources in `AAA` (but not vice versa).

![Trust Direction](https://github.com/user-attachments/assets/9743cd0d-776d-489f-9476-817b9b0736b6)

---

> Trust relationships do not automatically grant access. They simply allow for authorization between domains when needed. Permissions still need to be assigned explicitly.
---

## ✅ Task 9 - Conclusion

In this room, we’ve explored the foundational concepts of **Active Directory (AD)** and **Windows Domains** within a corporate environment.

---

### 🧠 What You’ve Learned

- What Active Directory is and how it works
- How Windows Domains simplify enterprise management
- Key AD components: users, groups, OUs, computers
- Delegation and permissions
- Group Policy Objects (GPOs) and their usage
- Authentication methods (Kerberos, NTLM)
- Multi-domain structures: Trees, Forests, Trusts

> 🔍 This room serves as an introduction to AD. There is much more to discover when deploying and securing AD in real-world environments.

---

### 🔐 What’s Next?

If you're interested in expanding your knowledge further:

- **🛡️ Secure your AD:**  
  TryHackMe - [Active Directory Hardening Room](https://tryhackme.com/room/adpractices)

- **🎯 Offensive Perspective:**  
  TryHackMe - [Compromising Active Directory Module](https://tryhackme.com/module/compromising-active-directory)

---

### 🙌 Final Thoughts

Congratulations on completing the Active Directory Basics room! 🎉  
You now have a solid understanding of how organizations manage users, computers, and security policies using Active Directory. Whether your goal is to become a **blue team defender** or a **red team attacker**, this knowledge forms an essential part of your cyber security journey.

Keep learning. Keep hacking. 💻🔐🚀
