# 🌐 Introduction to Web Hacking: Walking an Application

This documentation summarizes the **Walking An Application** module from the **Introduction to Web Hacking** path in TryHackMe's **Jr Penetration Tester** course.

![Walking an Application](https://github.com/user-attachments/assets/5e4c1877-27d2-4b1b-a20b-22e293da3f0a)

---

## 📌 Task 1: Overview

Learn manual web application security review using built-in browser tools:

* **View Source:** Human-readable source code
* **Inspector:** Inspect and modify page elements
* **Debugger:** Inspect JavaScript
* **Network:** Track page requests

---

## 📌 Task 2: Exploring The Website

Identify interactive parts of a website that could be vulnerable:

| Feature            | URL                     | Summary                                               |
| ------------------ | ----------------------- | ----------------------------------------------------- |
| Home Page          | `/`                     | Company info and staff photo                          |
| Latest News        | `/news`                 | List of news articles                                 |
| News Article       | `/news/article?id=1`    | Individual news articles; some require premium access |
| Contact Page       | `/contact`              | Customer contact form                                 |
| Customers          | `/customers`            | Redirects to login page                               |
| Customer Login     | `/customers/login`      | Login form                                            |
| Customer Signup    | `/customers/signup`     | User-signup form                                      |
| Customer Reset     | `/customers/reset`      | Password reset form                                   |
| Customer Dashboard | `/customers`            | User ticket list and creation                         |
| Create Ticket      | `/customers/ticket/new` | Form to create support ticket                         |
| Customer Account   | `/customers/account`    | Edit user details                                     |
| Customer Logout    | `/customers/logout`     | Logout                                                |

---

## 📌 Task 3: Viewing The Page Source

Inspect the HTML, CSS, and JavaScript source code for useful security insights:

![View Source Example](https://github.com/user-attachments/assets/6c0a1e28-28fd-412e-88a1-a9e8d02dcf50)

* **Comments:** May reveal useful or sensitive information
* **Hidden Links:** Can uncover private or confidential areas
* **Directory Listing:** Enabled listing reveals files that should be hidden
* **Framework Versions:** Identify outdated frameworks for known vulnerabilities

---

## 📌 Task 4: Developer Tools - Inspector

Use browser Inspector to:

![Inspector Premium Content Block](https://github.com/user-attachments/assets/8748e0a9-fddc-4040-941f-dd4fcd977720)
![Inspector Edit CSS](https://github.com/user-attachments/assets/5dc67c57-c880-4cb0-afee-46aa03c13c22)

* Identify HTML elements
* Edit CSS styles (e.g., remove content blockers like premium content paywalls)

*Example:* Change `display: block` to `display: none` to bypass content blocking.

---

## 📌 Task 5: Developer Tools - Debugger

Use Debugger for:

![flash](https://github.com/user-attachments/assets/9ac1cf30-31b1-4244-afe4-cf022b1c33a1)

* Examining and debugging JavaScript
* Utilizing breakpoints to pause JavaScript execution

*Example:* Find `flash['remove']();` and use a breakpoint to prevent red pop-up removal and reveal hidden messages or flags.

---

## 📌 Task 6: Developer Tools - Network

Use the Network tool to:

![Network](https://github.com/user-attachments/assets/b4c22015-1826-42bc-93ab-27bd8d4e344e)

* Monitor external requests from webpages
* Observe AJAX interactions to inspect form submissions and server responses

*Example:* Inspect AJAX network activity when submitting forms to discover hidden endpoints or flags.

---

## 🎯 Learning Objectives

* Master manual inspection techniques using built-in browser tools
* Identify hidden vulnerabilities in web applications
* Gain proficiency in using browser development tools

---

## 📚 Purpose of Documentation

This guide solidifies understanding of manual web security review methods using basic browser tools, useful for penetration testing and cybersecurity assessments.

---

🌟 **Continue learning and enhancing your cybersecurity skills!** 🌟

