# 🔐 IDOR (Insecure Direct Object Reference) Vulnerability

---

## 📌 **Task 1: What is an IDOR?**

An **Insecure Direct Object Reference (IDOR)** is an access control vulnerability. It occurs when a web application allows users to access objects (such as files, records, or database entries) by directly referencing them through user input without sufficient validation.

Essentially, an attacker can exploit this vulnerability by altering object identifiers (IDs) in requests to access unauthorized information.

---

## 📌 **Task 2: IDOR Example**

Imagine you've signed up for a website and accessed your profile via:

```
http://online-service.thm/profile?user_id=1305
```

You notice the parameter `user_id` can be manually changed. If you alter it to `1000`, like this:

```
http://online-service.thm/profile?user_id=1000
```

And you successfully view another user's information, you've discovered an IDOR vulnerability.

**Practical Action:**

* Always verify server-side that users only access their own objects.

---

## 📌 **Task 3: Finding IDORs in Encoded IDs**

IDs can sometimes be encoded (e.g., Base64). Consider the process below:

![Encoded IDOR Process](https://github.com/user-attachments/assets/bab8fda8-0020-4cb0-a4af-ab68dc74994b)

### Steps to Exploit:

1. **Decode** the encoded parameter (e.g., base64).

   * Encoded example: `eyJpZCI6MzB9`
   * Decoded result: `{ "id": 30 }`

2. **Tamper** with the decoded ID (e.g., change `30` to `10`).

   * Tampered result: `{ "id": 10 }`

3. **Encode** the modified data again to base64.

   * Re-encoded example: `eyJpZCI6MTB9`

4. **Submit** the altered request to access unauthorized resources.

Use [base64decode.org](https://www.base64decode.org/) and [base64encode.org](https://www.base64encode.org/) to test and exploit such vulnerabilities.

---

## 📌 **Task 4: Finding IDORs in Hashed IDs**

Sometimes, IDs appear as hashed values. For example, the ID `123` hashed using MD5 would become:

* MD5 hash: `202cb962ac59075b964b07152d234b70`

### Steps to Exploit:

* Use hash-cracking services like [CrackStation](https://crackstation.net/) to identify hashed IDs.
* Once decrypted, attempt altering the ID value and hashing it again to exploit the IDOR vulnerability.

---

## 📌 **Task 5: Finding IDORs in Unpredictable IDs**

If encoded or hashed IDs aren't easily identifiable, try the following:

* Create **two separate accounts**.
* Observe and swap IDs between these accounts.
* If swapping allows you to access another user's data, an IDOR vulnerability exists.

---

## 📌 **Task 6: Where are IDORs Located?**

IDOR vulnerabilities aren't limited to visible URL parameters. They can also be found in:

* AJAX calls (XHR requests visible in browser developer tools).
* JavaScript files containing API endpoints.
* Hidden parameters uncovered through **parameter mining**.

Example:

```
/user/details -> /user/details?user_id=123
```

Always investigate hidden or internal API requests thoroughly.

---

## 📌 **Task 7: Practical IDOR Example**

* Start by visiting the **Acme IT Support** website provided.
* **Create an account** and log in.
* Navigate to the **Your Account** tab.

Using browser developer tools (network tab), observe a request made to:

```
/api/v1/customer?id={user_id}
```

![Network Request IDOR](https://github.com/user-attachments/assets/f3f46bf8-ac6e-4876-a9d6-18c443d1fe52)

You can alter the `{user_id}` parameter to different values (e.g., `1` or `3`) to retrieve other users' data, confirming the IDOR vulnerability.

### Steps for Exploitation:

1. Intercept or observe the request in your browser.
2. Modify the ID parameter (`user_id`) to another known or guessed user ID.
3. Resubmit the request.
4. Successfully retrieve unauthorized user data.

---

## ✅ **Best Practices to Prevent IDOR:**

* Always validate user input server-side.
* Implement strict access control checks.
* Do not rely solely on obfuscation methods (hashing, encoding) for security.
* Conduct regular security testing and code reviews.

---

This detailed guide provides a comprehensive understanding of identifying, exploiting, and mitigating IDOR vulnerabilities.
