# 🌐 HTTP in Detail

This document summarizes the HTTP in Detail room on TryHackMe. It covers HTTP and HTTPS basics, URL structure, HTTP methods, status codes, headers, cookies, and more.

---

## 🧠 Task 1: What is HTTP(S)?

**HTTP (HyperText Transfer Protocol)** is a protocol used to load webpages and content (HTML, images, videos, etc.). It was developed by Tim Berners-Lee between 1989 and 1991.

**HTTPS (HyperText Transfer Protocol Secure)** is the encrypted version of HTTP. It ensures that:
- The communication is secure and private.
- You’re talking to the correct web server (not a fake).

### 🖼️ Image
![HTTP vs HTTPS](https://github.com/user-attachments/assets/434fb744-5e92-4ecc-83ce-cbb99ee9e389)

---

## 📥 Task 2: Requests and Responses

When you open a website, your browser makes **requests** for content like HTML, images, and scripts. The server responds with **responses**.

---

### 🔗 What is a URL?

A **URL (Uniform Resource Locator)** tells the browser where and how to access a web resource.

### 🖼️ Image  
![URL Structure](https://github.com/user-attachments/assets/2e2ae0bd-05ff-4428-82de-58d7c01177bb)
![URL Parts Explained](https://github.com/user-attachments/assets/6a1093d1-a765-4c37-ac54-ccd9f186dd96)
**URL Components:**
- **Scheme**: Protocol (http, https, ftp)
- **User**: Optional login credentials
- **Host**: Domain name or IP address
- **Port**: Defaults are 80 (HTTP), 443 (HTTPS)
- **Path**: File location (e.g., `/index.html`)
- **Query String**: Additional data (e.g., `?id=1`)
- **Fragment**: Section of the page (e.g., `#about`)

---

### 📡 Making a Request

You can make a request as simple as:
```http
GET / HTTP/1.1
```

But usually, you'll also send headers:

### 📄 Example Request:
![Example Request](https://github.com/user-attachments/assets/9d7cb5ce-e3ca-4952-92f6-e141482559c3)

### 📄 Example Response:
![Example Response](https://github.com/user-attachments/assets/cc85c03b-085b-481b-8367-c17333b13c2a)

---

## 🚦 Task 3: HTTP Methods

![HTTP Methods Diagram](스크린샷 2025-03-30 오전 10.09.40.png)

HTTP methods indicate what the client wants to do.

| Method  | Description |
|---------|-------------|
| **GET**    | Retrieve data |
| **POST**   | Send data (create new record) |
| **PUT**    | Send data (update existing record) |
| **DELETE** | Remove data or resource |

---

## ✅ Task 4: HTTP Status Codes

When a server responds, the first line includes a **status code**.

### 🔢 Status Code Categories:

| Code Range | Meaning |
|------------|---------|
| 100–199 | Informational |
| 200–299 | Success |
| 300–399 | Redirection |
| 400–499 | Client Error |
| 500–599 | Server Error |

### ⭐ Common Codes:
- **200 OK** – Request successful
- **201 Created** – Resource created
- **301 Moved Permanently** – URL changed permanently
- **302 Found** – Temporary redirect
- **400 Bad Request** – Invalid request
- **401 Unauthorized** – Not logged in
- **403 Forbidden** – No access
- **404 Not Found** – Page doesn't exist
- **405 Method Not Allowed** – Invalid HTTP method
- **500 Internal Server Error** – Unexpected server error
- **503 Service Unavailable** – Server overloaded or down

---

## 📦 Task 5: Headers

**Headers** provide additional data with requests and responses.

### 🔹 Common Request Headers:

| Header | Purpose |
|--------|---------|
| `Host` | Tells server which site to respond to |
| `User-Agent` | Browser and version |
| `Content-Length` | Size of the request body |
| `Accept-Encoding` | Supported compression methods |
| `Cookie` | Sends cookie data |

### 🔸 Common Response Headers:

| Header | Purpose |
|--------|---------|
| `Set-Cookie` | Tells browser to store cookie |
| `Cache-Control` | Controls caching behavior |
| `Content-Type` | Tells browser how to interpret data |
| `Content-Encoding` | Specifies compression method |

---

## 🍪 Task 6: Cookies

Cookies are small pieces of data sent by the server to your browser and stored locally. On future requests, your browser sends these cookies back.

### 🖼️ Image  
![Cookies Example](https://github.com/user-attachments/assets/1d847341-bdd9-4b61-b2c1-cbb81bf9a60b)

---

## 🛠️ Task 7: Making Requests

Practice building and sending HTTP requests using:
- Browser DevTools
- Postman
- `curl` (command line)
- TryHackMe's emulator

Use what you’ve learned: methods, headers, cookies, and status codes.

---

## 📚 Summary

- HTTP enables web communication, HTTPS secures it
- URLs define how and where to access resources
- HTTP Methods describe action: GET, POST, PUT, DELETE
- Status Codes explain request outcomes
- Headers and Cookies enrich and maintain web sessions
