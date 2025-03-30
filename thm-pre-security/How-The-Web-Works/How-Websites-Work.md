# 🌐 How Websites Work - TryHackMe Room Summary

This document summarizes the basics of how websites are structured and work, including front-end and back-end components, HTML, JavaScript, and common web vulnerabilities.

---

## 🧠 Task 1: How Websites Work

When you visit a website, your **browser** sends a request to a **web server**, and receives content back to render in your browser.

### 🖼️ Image
![How Websites Work](https://github.com/user-attachments/assets/ea6f63f9-f5e7-4cac-b617-14579697f5a5)

### Components:
1. **Front-End (Client-Side)** – What you see
2. **Back-End (Server-Side)** – Handles logic and data

---

## 🧾 Task 2: HTML

Websites are built using:
- **HTML** for structure
- **CSS** for design
- **JavaScript** for interactivity

### 🖼️ Image
![HTML Example Code](https://github.com/user-attachments/assets/ee310db1-afdb-43f0-8a61-eb631e3732a7)

### Example:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
  </head>
  <body>
    <h1>Example Heading</h1>
    <p>Example paragraph..</p>
  </body>
</html>
```

📌 Key HTML Elements:
•	<h1>: Heading
•	<p>: Paragraph
•	<img src="path">: Image
•	<button>: Button
•	class, id, src attributes used for styling, scripting, or media

---

## ⚙️ Task 3: JavaScript

**JavaScript (JS)** is one of the most popular coding languages in the world and allows web pages to become interactive.

While **HTML** defines the structure and content of a website, **JavaScript** controls its behavior and functionality. Without JavaScript, websites would be completely static and unresponsive to user actions.

JavaScript enables real-time updates, animations, and dynamic interactions — such as changing the style of a button when it is clicked or showing/hiding content based on user actions.

---

### 📌 How JavaScript is Added

JavaScript can be included in two ways:

- **Inline (in the HTML file)** using `<script>` tags:
```html
<script>
  // JS code here
</script>
```

- **External file** using the `src` attribute:
```html
<script src="/location/of/javascript_file.js"></script>
```
---

### 🧠 Example 1: Changing Text with JavaScript

This code finds a HTML element with the `id` of `demo` and changes its content:

```javascript
document.getElementById("demo").innerHTML = "Hack the Planet";
```

---

### 🧠 Example 2: Using HTML Events like `onclick`

HTML elements can have built-in events like `onclick` or `onhover`, which execute JavaScript when triggered.

The following button changes the text of the `demo` element to `"Button Clicked"` when clicked:

```html
<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>
  Click Me!
</button>
```

> ☝️ Note: These event handlers can also be defined inside a `<script>` block instead of directly in the HTML.

---

### ✅ Summary

- JavaScript gives life to static HTML.
- It's essential for making websites interactive.
- It can dynamically change content, styles, and trigger behavior on user actions like clicks or hovers.

---


## 🔐 Task 4: Sensitive Data Exposure

When sensitive data is left in source code, attackers may find it.

### 🖼️ Image
![Sensitive Info in HTML](https://github.com/user-attachments/assets/fa1b5141-8623-4f80-92b8-03d59552378b)

- Look for HTML comments with credentials
- Watch for admin links and exposed tokens

---

## ⚠️ Task 5: HTML Injection

Occurs when unsanitized user input is rendered into the page.

### 🖼️ Image
![HTML Injection Demo](https://github.com/user-attachments/assets/5d5c5cf5-8dd2-47b0-aa0d-3e255cfe4603)

Input like this:
```html
<h1>Hacked!</h1>
```
...and the site displays it as-is, the attacker controls part of the page.

### 🛡️ How to Prevent:
- Always sanitize user input before rendering it
- Strip or encode HTML tags (`<`, `>`, etc.)
- Use frameworks that auto-sanitize (React, Vue, etc.)

---

## ✅ Summary

- Websites use a client-server model: your browser (client) makes a request, and the server responds with HTML, CSS, JS, etc.
- HTML defines the layout; JavaScript powers interactions.
- Sensitive data should never appear in source code.
- Unsanitized input can lead to HTML Injection attacks.
