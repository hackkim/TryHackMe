# 🛡️ Introduction to Offensive Security

> “To outsmart a hacker, you need to think like one.”

**Offensive Security** is a field within cybersecurity that focuses on discovering and fixing system vulnerabilities from a hacker’s point of view.  
By identifying problems before real attackers do, organizations can significantly improve their security posture.

---

## 🧠 Task 1: What is Offensive Security?

![image](https://github.com/user-attachments/assets/fde5c0a4-f811-4d88-a48c-632c8dbca5f7)

Offensive Security involves:

- Gaining unauthorized access to computer systems  
- Exploiting software bugs  
- Discovering vulnerabilities in web applications  

In this **TryHackMe lab**, you'll legally and safely hack a simulated website to experience what it’s like to work as an **Ethical Hacker**.

---

## 💻 Task 2: Hacking Your First Machine

TryHackMe provides **Virtual Machines (VMs)** that simulate real-world environments, enabling hands-on learning.

In this task, you’ll hack a fake banking application called **FakeBank**.

---

### 🔘 Start the Machine

Click the **Start Machine** button to launch the environment.

> Your screen will split into two sections:  
> - The **left** side contains instructions  
> - The **right** side shows the running virtual machine  
>
> If the VM view disappears, click **Show Split View** at the top of the page to bring it back.

![Start Machine Screenshot](https://github.com/user-attachments/assets/3087b9da-f6c0-4d1d-bd63-6225e89f56de)

---

### 🌐 Step 0: Viewing the Target Website

Once the machine has started, a browser window will open displaying the FakeBank website:

![FakeBank Website](https://github.com/user-attachments/assets/a1679b25-bfd0-4b13-b18e-f6dc90018d0d)

This is a simulated online banking platform that shows user accounts and transaction data.

---

### 🧭 Step 1: Open a Terminal

On the virtual machine, click the **Terminal icon** on the right-hand side of the screen to open a terminal.

![Open Terminal](https://github.com/user-attachments/assets/ffd66390-ff64-41dd-a1d7-9953936a90b4)

The terminal is a command-line interface (CLI) that allows you to interact with the system using text commands.

---

### 🧰 Step 2: Discovering Hidden Pages with Gobuster

**Gobuster** is a command-line tool used to brute-force hidden directories and pages on a website.

In many real-world environments, developers accidentally leave sensitive admin portals or endpoints publicly accessible.  
As ethical hackers, our job is to identify those before attackers do.

Run the following command in the terminal to begin scanning the FakeBank website:

```bash
gobuster dir -u http://fakebank.thm -w wordlist.txt
```
The command will run and show you an output similar to this:

![image](https://github.com/user-attachments/assets/cc5b78de-a202-429a-8a92-a32deef6d5a3)

#### 🔍 Command Breakdown

| Option | Description |
|--------|-------------|
| `dir`  | Directory brute-force mode |
| `-u`   | Target website URL |
| `-w`   | Wordlist to use for scanning |

You will see that Gobuster scans the website with each word in the list, finding pages that exist on the site. Gobuster will have told you the pages in the list of page/directory names (indicated by Status: 200).

![image](https://github.com/user-attachments/assets/8858b805-7420-49df-9912-d541c56f2f2c)

### 💸 Step 3. Hack The Bank

You should have found a secret bank transfer page that allows you to transfer money between bank accounts (`/bank-transfer`). Type the hidden page into the FakeBank website using the browser's address bar.

![image](https://github.com/user-attachments/assets/c1397250-584b-43f9-a8a2-1c0178402a6e)

From this page, an attacker has authorized access and can steal money from any bank account. As an ethical hacker, you would (with permission) find vulnerabilities in their application and report them to the bank to fix them before a hacker exploits them.

Your mission is to transfer $2000 from bank account 2276 to your account (account number 8881). If your transfer was successful, you should now be able to see your new balance reflected on your account page.

Go there now and confirm you got the money! (You may need to hit Refresh for the changes to appear)

## 🚀 Task 3: Careers in Cyber Security

### 💼 How Can I Start Learning?

Many people ask:

- “How can I become a hacker (security consultant)?”  
- “How do I become a defender (security analyst fighting cybercrime)?”

The answer is **simple**:

> Choose an area you're interested in, and practice a little every day with hands-on exercises.

If you build the habit of learning daily with **TryHackMe**, you’ll develop the skills you need to get your **first job in cyber security**.

---

### 🌟 Real Success Stories

- **Paul**: Construction worker → Security engineer  
- **Kassandra**: Music teacher → Cybersecurity professional  
- **Brandon**: Used TryHackMe in school → Landed his first job in cyber

> 💬 “You can do it too!”

---

### 🔍 What Careers Are There?

Cyber security offers many career paths. Here are three key roles in **offensive security**:

- **Penetration Tester**  
  Tests technology products to find and report exploitable vulnerabilities.

- **Red Teamer**  
  Simulates real-world cyberattacks to assess how well an organization can detect and respond.

- **Security Engineer**  
  Designs, monitors, and maintains security systems to protect against attacks.

> Want to learn more? Check out the [Cyber Careers Room](https://tryhackme.com/room/cybercareers).

---

## ✅ Summary

In this lab, you:

- Learned what offensive security is
- Used Gobuster to discover hidden pages
- Found and accessed an insecure bank transfer page
- Explored how ethical hackers think
- Discovered career paths in cybersecurity

🎯 Keep practicing, stay curious, and hack ethically!
