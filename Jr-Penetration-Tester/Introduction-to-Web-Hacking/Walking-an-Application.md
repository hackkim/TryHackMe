# 🌐 Introduction to Web Hacking: Walking an Application

This documentation summarizes the **Walking An Application** module from the **Introduction to Web Hacking** path in TryHackMe's **Jr Penetration Tester** course.

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

* **Comments:** May reveal useful or sensitive information
* **Hidden Links:** Can uncover private or confidential areas
* **Directory Listing:** Enabled listing reveals files that should be hidden
* **Framework Versions:** Identify outdated frameworks for known vulnerabilities

---

## 📌 Task 4: Developer Tools - Inspector

Use browser Inspector to:

* Identify HTML elements
* Edit CSS styles (e.g., remove content blockers like premium content paywalls)

*Example:* Change `display: block` to `display: none` to bypass content blocking.

---

## 📌 Task 5: Developer Tools - Debugger

Use Debugger for:

* Examining and debugging JavaScript
* Utilizing breakpoints to pause JavaScript execution

*Example:* Find `flash['remove']();` and use a breakpoint to prevent red pop-up removal and reveal hidden messages or flags.

---

## 📌 Task 6: Developer Tools - Network

Use the Network tool to:

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
