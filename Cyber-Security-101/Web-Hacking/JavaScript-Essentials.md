# 🌐 JavaScript Essentials (TryHackMe)

---

## Task 1: Introduction

JavaScript (JS) is a widely-used scripting language that allows developers to add interactive and dynamic features to websites built using HTML and CSS. It powers the behavior of web pages in the browser.

![JavaScript on Laptop](https://github.com/user-attachments/assets/ac695c35-47bc-47e0-aa04-2c59ddeb0436)
![VM Exercise Folder](https://github.com/user-attachments/assets/f62409f8-e810-409f-90ed-f0cc99929c9c)

### 📌 Why Learn JavaScript?
- It enables form validation, animations, alerts, and more.
- It’s essential in both development and offensive security (for XSS and other attack simulations).

### 🎯 Room Prerequisites
- Linux Fundamentals
- Web Application Basics
- How Websites Work

### 🎯 Learning Objectives
- Understand JS fundamentals
- Integrate JS in HTML (internally/externally)
- Explore browser interactions
- Recognize abuse cases (e.g., alerts, prompts)
- Analyze obfuscated JS
- Follow JS security best practices

---

## Task 2: Essential Concepts

### 📦 Variables

Variables are named containers for storing data.  
Three types in JS:

![var vs let vs const](https://github.com/user-attachments/assets/57a10a1e-96e2-46d8-acc1-a80f93b54939)

- `var`: function-scoped
- `let`: block-scoped (preferred)
- `const`: block-scoped and immutable

### 📦 Data Types

- `String`, `Number`, `Boolean`, `Null`, `Undefined`, `Object`, `Array`

### 📦 Functions

Group related code together to reuse it.

```javascript
function PrintResult(rollNum) {
  alert("Username with roll number " + rollNum + " has passed the exam");
}
```

### 📦 Loops

Automate repetitive tasks.

```javascript
for (let i = 0; i < 100; i++) {
  PrintResult(rollNumbers[i]);
}
```

### 📦 Request-Response Cycle

Web clients send HTTP requests, and web servers return responses (pages, data, etc).

---

## Task 3: JavaScript Overview

JavaScript is **interpreted** in the browser.

```javascript
console.log("Hello, World!");

let age = 25;
if (age >= 18) {
  console.log("You are an adult.");
} else {
  console.log("You are a minor.");
}

function greet(name) {
  console.log("Hello, " + name + "!");
}
greet("Bob");
```

### 🛠 Running in Chrome Console

![Chrome Desktop](https://github.com/user-attachments/assets/cd6bf198-873b-48ec-b961-3bea1844f0ec)  
![Right Click Inspect](https://github.com/user-attachments/assets/06204cc7-7961-4822-ad2b-a92a53568753)  
![Console Tab Opened](https://github.com/user-attachments/assets/336a444e-1117-40e9-b525-9aded82bb165)  
![JS Console Output](https://github.com/user-attachments/assets/d71d2fc6-3853-4e89-b844-cf24e93c4171)

---

## Task 4: Integrating JavaScript in HTML


![Open internal.html with Pluma](https://github.com/user-attachments/assets/d15ac154-2b36-4465-b3a2-5455349e0814)
![Internal JS result in browser](https://github.com/user-attachments/assets/88adef5f-732e-4c19-b1b1-e07c2b2e1382)
![External JS result in browser](https://github.com/user-attachments/assets/0e66dbb2-2e42-401b-a8a5-b0b72cd1651c)
![Right-click View Page Source](https://github.com/user-attachments/assets/90dd64b6-fb95-4152-95fb-709f5add1338)
![HTML shows external JS src](https://github.com/user-attachments/assets/1960f194-c77d-4fba-9b37-5aae80831652)
![External JS loaded from TryHackMe](https://github.com/user-attachments/assets/38597748-dc23-4b6b-9b76-0c5adfa10d6e)


### 🧩 Internal JS
```html
<script>
  let x = 5, y = 10;
  document.getElementById("result").innerHTML = "The result is: " + (x + y);
</script>
```

### 🧩 External JS
```html
<script src="script.js"></script>
```

### 🔍 Detect Internal vs External
- Use `View Page Source`
- `script` tag without `src` = internal
- `script` tag with `src` = external

---

## Task 5: Abusing Dialogue Functions


![JS alert example](./alert_hello_thm.png)
![JS prompt example](./prompt_name_input.png)
![JS confirm example](./confirm_dialog.png)
![JS alert hacked file](./invoice_alert_hacked.png)


Built-in dialogue functions:
- `alert("Hello THM");`
- `prompt("What is your name?");`
- `confirm("Are you sure?");`

Malicious example:
```html
<script>
  for (let i = 0; i < 3; i++) {
    alert("Hacked");
  }
</script>
```

Attackers can abuse these to annoy or confuse users.

---

## Task 6: Bypassing Control Flow Statements


![Age Prompt Verification](./age_verification_prompt.png)
![login.html File](./login_file_highlighted.png)
![Login Authenticated Page](./login_auth_success.png)


Example:
```html
<script>
  let age = prompt("What is your age?");
  if (age >= 18) {
    document.getElementById("message").innerHTML = "You are an adult.";
  } else {
    document.getElementById("message").innerHTML = "You are a minor.";
  }
</script>
```

### 🛑 Insecure JS Login Logic

Users can modify JS login logic if implemented client-side.  
Always validate authentication server-side.

---

## Task 7: Exploring Minified Files


![Alert from hello.html](./hello_html_alert_welcome.png)
![hello.js visible in Sources tab](./hello_js_browser_sources.png)
![Online JS Obfuscator](./js_obfuscator_tool.png)
![Obfuscated JS loaded in browser](./browser_loaded_obfuscated_code.png)
![JS deobfuscator result](./deobfuscator_result_example.png)


### ✅ Minification
Removes whitespace, comments to reduce size.

### ❌ Obfuscation
Makes code unreadable intentionally.

Original:
```javascript
function hi() {
  alert("Welcome to THM");
}
hi();
```

Obfuscated:
```javascript
(function(){/* gibberish */})()
```

Use browser DevTools → Sources tab to inspect loaded JS files.

---

## Task 8: Best Practices

✅ Do this:
- Validate data server-side
- Use trusted libraries
- Obfuscate & minify code for production

🚫 Avoid:
```javascript
const apiKey = "super-secret-key"; // ❌ Never hardcode secrets
```

---

## Task 9: Conclusion

🎉 Congrats on completing the JavaScript Essentials room!

### You Learned:
- JS syntax & browser integration
- Client-side logic & abuse vectors
- Obfuscation techniques
- Secure development practices

➡️ Keep learning. Your JS hacking journey is just getting started!


---

## Task 8: Best Practices

When developing or testing JavaScript-based websites, it is important to reduce the attack surface and follow secure coding practices.

### ✅ Avoid Relying Solely on Client-Side Validation
JavaScript validations can be bypassed. Always validate inputs again on the server side.

### ✅ Refrain from Including Untrusted Libraries
Avoid blindly using JS libraries found on the internet. Malicious actors upload look-alike packages to trick developers.

### ❌ Avoid Hardcoded Secrets
Never embed secrets like API keys or tokens into frontend JS:
```javascript
// Bad practice
const privateAPIKey = 'pk_TryHackMe-1337';
```

### ✅ Minify and Obfuscate Code
Helps protect logic and reduces file size. However, **do not rely solely on obfuscation** for security.

---

## Task 9: Conclusion

🎉 **Congratulations on completing the JavaScript Essentials room!**

You’ve explored:
- JavaScript basics and syntax
- Dialogue function abuses (`alert`, `prompt`, `confirm`)
- JS integration into HTML
- Control flow logic and bypass scenarios
- Code obfuscation and deobfuscation
- Secure JS coding best practices

🔐 Keep these skills sharp to defend against real-world web threats.  
Your journey in mastering secure JavaScript has just begun!

💬 Let us know your thoughts on this room in our [Discord](https://discord.gg/tryhackme) or on our X (Twitter) page.
