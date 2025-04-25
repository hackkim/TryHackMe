# 🌐 Web Application Basics (TryHackMe)

## Task 1: Introduction

![Task 1 Intro](https://github.com/user-attachments/assets/8e124514-b543-4fca-8e83-04d120493f54)

Welcome to Web Application Basics! In this room, we’ll walk through the key elements of a web application, such as URLs, HTTP requests, and responses. This is perfect if you're starting and want to get a handle on the essentials or if you're looking to build or work with web apps.

### 🎯 Learning Objectives

- Understand what a web application is and how it runs in a web browser.
- Break down the components of a URL and see how it helps access web resources.
- Learn how HTTP requests and responses work.
- Get familiar with the different types of HTTP request methods.
- Understand what different HTTP response codes mean.
- Check out how HTTP headers work and why they matter for security.

---

## Task 2: Web Application Overview

![Task 2 Overview](https://github.com/user-attachments/assets/30b8d469-967d-46fa-a645-43ed078b8b4c)

Web apps can be thought of like planets. We interact with their front ends like astronauts exploring surfaces, while the complex back end (servers, databases, infrastructure) lies beneath.

- **HTML** defines content structure (like DNA).
![HTML](https://github.com/user-attachments/assets/93d588af-f239-400d-a5ef-338d966aaf10)
- **CSS** defines style (like appearance).
![CSS](https://github.com/user-attachments/assets/11f6e871-7baf-4951-815c-2a8b20b6615e)
- **JavaScript** enables interactivity (like a brain).
![JS](https://github.com/user-attachments/assets/0645c521-fe95-4bca-8a2b-0effb3383548)

Back-end components include:
- **Databases** for storage and retrieval.
![DB](https://github.com/user-attachments/assets/bf503cd5-1d24-469b-a984-bf8fd003fbde)
- **Infrastructure** like servers, networking, etc.
![Infrastructure](https://github.com/user-attachments/assets/63f110fe-69bf-46e2-8ce6-ad4a6e6b8629)
- **WAF (Web Application Firewall)** for filtering malicious traffic.
- ![WAF](https://github.com/user-attachments/assets/2936130b-cf35-4f2a-b158-eebb71998d1b)

---

## Task 3: Uniform Resource Locator

![URL Diagram](https://github.com/user-attachments/assets/e130abc7-6d45-44cf-8814-c52943ee340f)

A **URL** is a web address for resources like web pages, images, or videos.

### 📌 Components

- **Scheme**: Protocol (HTTP, HTTPS)
- **User Info**: Login credentials (rare)
- **Host/Domain**: Website address
- **Port**: Network port (e.g., 80, 443)
- **Path**: File location on server
- **Query String**: Data passed in URL
- **Fragment**: Section on the page

---

## Task 4: HTTP Messages

![HTTP Messages](https://github.com/user-attachments/assets/1caa4eea-42ab-4193-9098-01391eac101b)

HTTP messages are how clients and servers talk.

- **Request**: Sent by the client (e.g., GET /login)
- **Response**: Server's reply (e.g., 200 OK)

Each includes:
- **Start Line**
- **Headers**
- **Body**
- **Blank line** to separate headers/body

---

## Task 5: HTTP Request – Request Line and Methods

![http_request_structure_explained.png](https://github.com/user-attachments/assets/08bd14fd-99c7-4fe0-a132-62ac002f1fb4)

The **Request Line** contains:

- HTTP Method (GET, POST, PUT, DELETE, etc.)
- Path to the resource (e.g. `/login`)
- HTTP Version (e.g. `HTTP/1.1`)

Each method has a different use and potential security considerations.

---

## Task 6: HTTP Request – Headers and Body


**Request Headers** give the server additional information:

- Host
- User-Agent
- Content-Type
- Cookie
- Referer

**Request Body** holds data for POST/PUT requests in various formats:

- x-www-form-urlencoded
- multipart/form-data
- JSON
- XML

---

## Task 7: HTTP Response – Status Line and Status Codes

![http_status_codes_200_404_500.png](https://github.com/user-attachments/assets/e477e0b2-347c-4766-a057-bd3615a68242)

The **status line** shows:

- HTTP Version
- Status Code
- Reason Phrase

### Common Status Codes

- `200 OK`: Success
- `301 Moved Permanently`: Redirection
- `404 Not Found`: Client error
- `500 Internal Server Error`: Server issue

---

## Task 8: HTTP Response – Headers and Body

![http_response_structure_explained.png](https://github.com/user-attachments/assets/cb4ced75-4bc7-473b-95b2-360fdad04fa4)

**Response Headers** like:

- `Content-Type`: format of returned content
- `Content-Length`
- `Date`
- `Server`
- `Set-Cookie`
- `Cache-Control`
- `Location`

**Response Body**: main content returned (HTML, JSON, images, etc.)

---

## Task 9: Security Headers

Security headers protect users and apps.

- `Content-Security-Policy`: Controls allowed content sources
- `Strict-Transport-Security`: Forces HTTPS
- `X-Content-Type-Options`: Prevent MIME type guessing
- `Referrer-Policy`: Controls referrer information shared

Check site headers: https://securityheaders.io/

---

## Task 10: Practical Task – Making HTTP Requests

Use the built-in split-view static site to interact with an HTTP emulator and apply what you’ve learned.

---

## Task 11: Conclusion

![Conclusion](https://github.com/user-attachments/assets/4b17f7e4-fb7d-498a-965b-b5f96a53cf07)

🎉 You’ve completed Web Application Basics!

### You now understand:

- Web app structure
- URL anatomy
- HTTP request and response flow
- Header significance
- Security hardening via HTTP headers

Happy hacking! 🧠🚀

📝 Platform: [TryHackMe](https://tryhackme.com)
