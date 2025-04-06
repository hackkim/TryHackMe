## 🪟 TryHackMe - Active Directory Basics
---
### 🧭 Task 1 - Introduction

Active Directory (AD) is Microsoft's directory service that is foundational in most enterprise environments.  
It simplifies and centralizes the management of users, computers, resources, and security policies.

---

### 🎯 Room Objectives

By the end of this room, you will understand:

- What Active Directory is
- The concept of a Windows Domain
- Key components in an AD domain (users, machines, OUs, groups)
- Forests, Trees, and Trust Relationships
- How authentication and delegation work
- Group Policy Objects (GPOs)

---

### 📌 Use Cases

Active Directory is used in schools, universities, corporations, and government networks.  
If you've ever logged into a shared school or work computer with the same credentials,  
you’ve likely interacted with Active Directory.

---

### 🔧 Room Prerequisites

Before beginning, it is recommended to:

- Have basic Windows OS knowledge  
  👉 Review the **Windows Fundamentals 1–3** modules if needed.

---

### 🧪 Lab Setup

In this room, you will take the role of an IT administrator at **THM Inc.**  
You’ll review and configure the existing domain environment: `THM.local`.

- The domain controller is preconfigured.
- You'll connect to the virtual machine via **RDP** or web browser.
- The machine will be reused for all tasks.

📌 Credentials:  
- **Username:** `THM\Administrator`  
- **Password:** `Password321`

📌 Start the AttackBox (or use your own RDP client) before beginning.

![RDP Login Example](./images/screenshot_rdp_login.png)

---

Let’s get started by exploring what a Windows Domain really is in Task 2!

---
## 🏢 Task 2 - Windows Domains

Imagine you're managing a small business with only five employees and five computers.  
You can probably configure everything manually — log into each machine, set up users, apply local settings, etc.

But what happens when your company grows to **hundreds of users and devices** across multiple locations?

---

### 🧠 The Need for a Windows Domain

A **Windows Domain** centralizes identity and access management using **Active Directory (AD)**.  
All users, machines, and policies are controlled from one place — the **Domain Controller (DC)**.

📌 Domain-based network structure:  
![Windows Domain Diagram](./images/screenshot_windows_domain_topology.png)

---

### 🎯 Key Benefits

- **Centralized Identity Management**  
  All user accounts and permissions are managed from a single server (DC)

- **Policy Management**  
  Set security and usage policies that apply to all or specific users/machines

- **Efficiency at Scale**  
  Easy to onboard/offboard employees, manage passwords, or apply changes globally

---

### 🧪 Real-World Example

In many schools or companies, you receive a username and password that works on **any PC in the network**.  
You’re authenticated against the Active Directory — not the local machine.

- Password resets apply network-wide  
- Access is controlled by policies set on the Domain Controller  
- You can't open the control panel? That's GPO in action

---

### 🔧 Your Lab: Welcome to THM Inc.

You're the new IT admin at **THM.local**, a Windows Domain with multiple departments.

To explore the AD environment:

1. Start the attached TryHackMe machine
2. Connect via browser or RDP

📌 RDP Credentials:

- **Username:** `THM\Administrator`  
- **Password:** `Password321`

![RDP Credentials Example](./images/screenshot_rdp_credentials.png)

> ✅ Be sure to start the machine early. It will be used across all tasks.

---

Next, we’ll dive into the actual structure and objects of Active Directory in Task 3.

---

## 🧩 Task 3 - Active Directory

The core of any Windows Domain is **Active Directory Domain Services (AD DS)**.  
This service stores and manages information about all the "objects" on the network.

Objects include:

- Users
- Machines
- Groups
- Printers
- Shared folders
- Organizational Units (OUs)

---

### 👤 Users

Users are **security principals**, meaning they can be authenticated and assigned permissions.  
They may represent:

- People (employees)
- Services (like MSSQL, IIS)

📌 Example: User Management  
![AD Users](./images/screenshot_ad_users.png)

---

### 🖥️ Machines

Each domain-joined computer becomes a **machine object** in AD.  
It has limited rights but is a security principal and can log in.

- Naming convention: `COMPUTERNAME$`
- Passwords are auto-rotated every 30 days

📌 Example: OU View  
![OU View](./images/screenshot_ad_ou_view.png)

---

### 👥 Security Groups

Groups are used to assign permissions to multiple users or machines at once.  
They can be nested (group inside a group), and also include computers.

📌 Example: User List  
![AD User List](./images/screenshot_ad_user_list.png)

#### 🔐 Default Security Groups

| Security Group        | Description |
|-----------------------|-------------|
| Domain Admins         | Full control over the domain |
| Server Operators      | Can manage DCs, not groups |
| Backup Operators      | Can access all files for backup |
| Account Operators     | Can manage user accounts |
| Domain Users          | All user accounts in the domain |
| Domain Computers      | All computers in the domain |
| Domain Controllers    | All Domain Controllers |

---

### 🗂️ Organizational Units (OUs)

OUs are containers that help organize AD objects logically.

- OUs are used to apply Group Policies
- A user can belong to only one OU at a time
- Users can belong to many groups

📌 Example: OU Hierarchy  
![OU Hierarchy](./images/screenshot_ad_ou_tree.png)

---

### 🔁 OUs vs Security Groups

| Feature      | Security Groups             | Organizational Units (OUs)     |
|--------------|------------------------------|---------------------------------|
| Purpose      | Assign permissions           | Apply policies                  |
| Membership   | Users can join multiple      | Users belong to one             |
| Example Use  | Grant shared folder access   | Apply password complexity rules |

> ✅ OUs = Policy Management  
> ✅ Groups = Permission Management

---

Now that you understand how AD stores and organizes objects, let's manage them in Task 4.

---

## 🔧 Task 4 - Managing Users in Active Directory

As the new domain administrator at THM Inc., your first task is to clean up the Active Directory (AD) users and OUs to reflect the current organizational structure.

---

### 🧭 Organizational Chart

Here’s the updated org chart you need to align the AD structure with:

![Org Chart](./images/screenshot_task4_org_chart.png)

---

### 🗑️ Deleting Extra OUs

You'll notice some outdated OUs in the domain structure. When trying to delete one of them, you’ll receive an error:

![Deletion Error](./images/screenshot_task4_delete_error.png)

---

To remove the OU, first enable **Advanced Features**:

![Advanced Features](./images/screenshot_task4_advanced_features.png)

---

Then, uncheck **Protect object from accidental deletion**:

![Uncheck Protection](./images/screenshot_task4_uncheck_protection.png)

---

### 🧑‍💼 Delegating OU Control

You want Phillip (IT Support) to reset passwords in the Sales, Marketing, and Management OUs.

Right-click the OU (e.g., Sales) and select **Delegate Control...**:

![Delegate Control](./images/screenshot_task4_delegate_control.png)

---

Use **Add** and **Check Names** to select the `phillip` user:

![Add Phillip](./images/screenshot_task4_add_phillip.png)

---

In the next step, choose **Reset user passwords and force password change at next logon**:

![Choose Reset Password](./images/screenshot_task4_choose_reset.png)

---

### 🧪 Verifying with Phillip's Account

Phillip's credentials:

![Phillip Credentials](./images/screenshot_task4_phillip_creds.png)

Use PowerShell to reset Sophie’s password:

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
