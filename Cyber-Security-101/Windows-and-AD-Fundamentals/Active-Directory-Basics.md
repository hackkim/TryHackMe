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

As a new AD Administrator, you’ve received a request to **review and update the Organizational Units (OUs)** and users to match the updated org chart.

---

### 📋 Step 1: Review the Org Chart

📌 Organizational Chart  
![Org Chart](https://github.com/user-attachments/assets/d6b7e103-0f7f-4437-bf42-4ebd61ad0451)

---

### 🧹 Step 2: Delete Unused OUs

You’ll notice an extra department in AD not shown in the org chart. Try to delete it, but…

📌 Error When Deleting OU  
![Delete Error](https://github.com/user-attachments/assets/f48d8f81-a8a2-45b2-9e0e-2f6a2522427d)

---

By default, OUs are protected from accidental deletion.

✅ To delete the OU:

1. Enable **Advanced Features** from the `View` menu.

📌 Enable Advanced Features  
![Advanced Features](https://github.com/user-attachments/assets/ab404e80-708a-40d2-8b9d-c7337d86c1b3)

2. Open OU properties → `Object` tab → Uncheck **Protect object from accidental deletion**.

📌 Disable OU Protection  
![Disable Protection](https://github.com/user-attachments/assets/52f32b97-3778-496a-b834-b101a88b1544)

3. Delete the OU again – it will succeed.

---

### ➕ Step 3: Create or Delete Users

Ensure each department has the correct users.

📌 OU and User View  
![OU Tree](https://github.com/user-attachments/assets/704dbb97-94bf-4091-be70-a48e85a91e89)  
![Users in OU](https://github.com/user-attachments/assets/7394f7e4-b0c1-47db-919b-e19119c3dd27)

---

### 👤 Step 4: Delegate Password Reset Privileges

Let’s **delegate password reset permissions** to Phillip (IT Support) for the `Sales OU`.

📌 Delegate Control  
![Delegate OU](https://github.com/user-attachments/assets/10493208-a771-4db3-9a72-7cb13de4ecdf)

---

1. Add `phillip` as the delegated user.

📌 Add User  
![Add Phillip](https://github.com/user-attachments/assets/9564fdfd-256a-499a-a7dd-09522efd8177)

2. Choose **Reset passwords** permission.

📌 Select Reset Task  
![Reset Password Option](https://github.com/user-attachments/assets/2caad36b-7183-4c62-9c3b-73ee964d3ac0)

---

### 🔑 Try Phillip’s New Permissions

Login as Phillip:

📌 Phillip's Credentials  
![Phillip Login](./images/screenshot_ad_phillip_creds.png)

- **Username**: `THM\phillip`  
- **Password**: `Claire2008`

---

### 🧪 PowerShell: Reset Sophie’s Password

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

![Default Computers Container](./images/screenshot_ad_computers_list.png)

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

![Created OUs](./images/screenshot_ad_created_ous.png)

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

![Group Policy Management](./images/screenshot_group_policy_launch.png)

---

### 🧱 Creating and Linking GPOs

GPOs are created under **Group Policy Objects** and then linked to Organizational Units (OUs) to take effect.

![GPOs created and linked](./images/screenshot_gpo_linked.png)

---

### 🔎 Viewing GPO Scope

Each GPO has a **Scope** tab that shows where the policy is linked and who it applies to.

![Scope tab](./images/screenshot_gpo_scope.png)

---

### ⚙️ Viewing GPO Settings

The **Settings** tab shows which policies are active under Computer or User Configuration.

![GPO Settings tab](./images/screenshot_gpo_settings_tab.png)

---

### 🔐 Default Domain Policy Example

The **Default Domain Policy** typically includes password policies and lockout settings.

![Default domain policy details](./images/screenshot_default_domain_policy.png)

---

### ✏️ Editing GPOs

To modify a GPO, right-click and choose **Edit**.

![Edit GPO](./images/screenshot_edit_gpo.png)

---

### 🔏 Enforcing Password Complexity

Navigate to the password policy settings and adjust options like **minimum password length**.

![Minimum password length](./images/screenshot_password_length.png)

---

### ❓ Learn More via 'Explain' Tab

Use the **Explain** tab to read detailed descriptions of each setting.

![Explain tab](./images/screenshot_explain_password_setting.png)

---

## 🎯 Restrict Control Panel Access

Create a new GPO and enable the setting:

**User Configuration → Admin Templates → Control Panel → Prohibit access to Control Panel and PC settings**

![Prohibit Control Panel Access](./images/screenshot_restrict_control_panel.png)

---

### 🔗 Link GPO to Targeted OUs

Apply this GPO only to OUs that require restrictions (e.g., Sales, Management).

![Linking Control Panel GPO](./images/screenshot_link_gpo_control_panel.png)

---

## 🖥️ Auto Lock Screen GPO

Create a GPO to automatically lock the screen after inactivity.

**Computer Configuration → Policies → Windows Settings → Security Settings → Local Policies → Security Options → Interactive logon: Machine inactivity limit**

Set to **300 seconds (5 minutes)**.

![Auto Lock Screen setting](./images/screenshot_machine_inactivity_limit.png)

---

### 🔗 Linking Auto Lock Screen GPO

Link the Auto Lock Screen policy to the domain so it affects all workstations.

![Auto Lock Screen GPO linked](./images/screenshot_auto_lock_linked.png)

---

### 🔐 Testing as a User

Login using a test user (e.g., Mark) to confirm that restrictions and lockouts are working properly.

![Mark credentials](./images/screenshot_mark_credentials.png)

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
![Kerberos Step 1 - Request TGT](./images/kerberos_step1_request_tgt.png)

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
![Kerberos Step 2 - Request TGS](./images/kerberos_step2_request_tgs.png)

The KDC responds with:

- A **TGS** for the service, encrypted with the service owner's password hash
- A **service session key**

---

### 🖥️ 3. Authenticating to the Service

The client sends the **TGS** and an encrypted **timestamp** to the target service to prove identity.

📌  
![Kerberos Step 3 - Authenticate to Service](./images/kerberos_step3_authenticate.png)

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
![NetNTLM Flow](./images/netntlm_authentication_flow.png)

> ⚠️ Password hashes are never sent across the network in plain text.

---
## 🌳 Task 8 - Trees, Forests, and Trusts

In large enterprise environments, a single domain might not be sufficient. Microsoft’s Active Directory allows organizing domains into trees and forests and managing trust relationships between them.

---

### 🏢 Single Domain Structure

A basic domain structure consists of a domain controller and other systems (file server, workstation, etc.) under one namespace.

![Domain Structure](./images/screenshot_task8_domain.png)

---

### 🌲 Domain Trees

A tree is a collection of domains that share a contiguous namespace. For example:

- Root domain: `thm.local`
- Child domains: `uk.thm.local`, `us.thm.local`

Each domain can be administered independently, but they’re part of the same tree.

![Tree Structure](./images/screenshot_task8_tree.png)

---

### 🌳 Forests

A forest is a collection of trees that do not necessarily share the same namespace. Each tree in the forest can contain multiple domains.

Example:
- `thm.local` tree (with `uk.thm.local`, `us.thm.local`)
- `mht.local` tree (with `eu.mht.local`, `asia.mht.local`)

Together they form a forest.

![Forest Structure](./images/screenshot_task8_forest.png)

---

### 🔐 Trust Relationships

Trusts allow users in one domain to access resources in another domain.

- 🔄 Two-way trust: Both domains trust each other.
- 🔁 One-way trust: Only one domain trusts the other.

For example:
If `Domain AAA` trusts `Domain BBB`, users in `BBB` can access resources in `AAA` (but not vice versa).

![Trust Direction](./images/screenshot_task8_trust.png)

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
