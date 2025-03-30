# 🧩 Putting It All Together - TryHackMe Room Summary

A final summary of how the web works behind the scenes — from DNS to HTTP, to web servers and supporting components.

---

## 🧠 Task 1: Putting It All Together

When you request a website, a lot goes on behind the scenes:

1. Your browser looks up the server's IP address using **DNS**.
2. Your browser connects to the server using the **HTTP** protocol.
3. The server responds with content: **HTML**, **CSS**, **JavaScript**, **images**, etc.
4. The browser renders the page using this data.

### 🖼️ Image  
![Putting It All Together](https://github.com/user-attachments/assets/74d82516-d07a-4852-b6e7-057f746d47e4)

There are also additional components that help make the web faster, more scalable, and more secure.

---

## ⚙️ Task 2: Other Components

### 🔁 Load Balancers

Load balancers help high-traffic websites by:

- Distributing traffic across multiple servers
- Providing failover in case a server goes down

**Algorithms used:**
- **Round-robin** – Rotate evenly between servers
- **Weighted** – Send traffic to the least busy server

They also run **health checks** to ensure servers are functioning.

### 🖼️ Image  
![Load Balancer Flow](https://github.com/user-attachments/assets/b195ad84-3e72-4f16-b659-a0ea4e1b79f1)

---

### 🌍 CDN (Content Delivery Network)

- Hosts static files (CSS, JS, images, etc.) on global servers
- Delivers content from the **nearest** physical location
- Reduces server load and latency

---

### 💾 Databases

- Stores persistent data like user accounts, posts, orders
- Can be small (text files) or large (distributed clusters)
- Examples: **MySQL**, **MSSQL**, **MongoDB**, **PostgreSQL**

---

### 🛡️ WAF (Web Application Firewall)

- Filters requests before they hit the server
- Protects from:
  - **DDoS attacks**
  - **Hacking attempts**
  - **Bots**
- Uses techniques like **rate limiting**

### 🖼️ Image  
![Web Application Firewall](https://github.com/user-attachments/assets/420a7286-d73f-4d8d-a558-26d648081df9)

---

## 🖥️ Task 3: How Web Servers Work

### 🌐 What is a Web Server?

A **web server** is software that listens for incoming HTTP connections and delivers content.

**Common web servers:**
- **Apache**
- **Nginx**
- **IIS**
- **NodeJS**

They serve files from a **root directory**, like:

- Linux: `/var/www/html`
- Windows: `C:\inetpub\wwwroot`

Example:  
Requesting `http://example.com/image.jpg` retrieves `/var/www/html/image.jpg`.

---

### 🗂️ Virtual Hosts

Allow a single web server to host **multiple domains**.

- Based on the **hostname** in the HTTP request
- Mapped in configuration files
- Each site has its own root directory:
  - `one.com` ➝ `/var/www/website_one`
  - `two.com` ➝ `/var/www/website_two`

---

### 🧱 Static vs Dynamic Content

| Static Content                          | Dynamic Content                                   |
|----------------------------------------|--------------------------------------------------|
| Doesn't change                         | Generated in real-time based on user/data input |
| Examples: images, CSS, static HTML     | Examples: blog homepage, search results          |
| Served directly from disk              | Processed via server-side logic                  |

---

### 🖥️ Backend Languages

Used to build dynamic, interactive sites by processing logic and connecting to databases.

**Popular backend languages:**
- PHP
- Python
- Ruby
- NodeJS
- Perl

---

### 🧪 Example: Simple PHP Page

URL:  
`http://example.com/index.php?name=adam`

**index.php**
```php
<html><body>Hello <?php echo $_GET["name"]; ?></body></html>
```

**Output to the client:**
```html
<html><body>Hello adam</body></html>
```

You'll notice that the client doesn't see any PHP code because it's on the **Backend**.  
This interactivity opens up a lot more security issues for web applications that haven’t been created securely, as you’ll learn in further modules.

---

## 🧩 Task 4: Quiz

Click the **"View Site"** button to complete a drag-and-drop quiz.
