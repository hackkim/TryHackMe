# Burp Suite: Intruder

---

## 📌 Task 1: Introduction

Welcome to the **Burp Suite Intruder** guide!

In this guide, we delve into Burp Suite's Intruder, exploring automation capabilities for fuzzing, brute-forcing, and other security tests.

Ensure Burp Suite and the target VM are activated before proceeding.

---

## 📌 Task 2: What is Intruder?

**Intruder** is Burp Suite’s module for automating and customizing attacks, useful for:

- Brute-forcing login forms (credential stuffing)
- API endpoint fuzzing
- Parameter vulnerability tests

**Intruder Interface Overview:**

![Intruder Interface](https://github.com/user-attachments/assets/1bf46e01-34b2-4bea-b68b-c7aa2ddb51a8)

---

## 📌 Task 3: Positions

Positions define where payloads will be injected in requests:

- **`§` symbols** indicate injection points.
- **Auto§**: Automatically identifies payload positions.
- **Add§ / Clear§**: Manually manage payload positions.

**Managing Positions Examples:**

- Adding positions manually:  
![Positions Setup](https://github.com/user-attachments/assets/78780fc4-c900-420a-a4c9-0c581beaafe2)

- Clearing existing positions:  
![Positions Clearing](https://tryhackme-images.s3.amazonaws.com/user-uploads/645b19f5d5848d004ab9c9e2/room-content/504d75f7c90e1c985dae5e05038f50ac.gif)

---

## 📌 Task 4: Payloads

Payloads tab configures values inserted during attacks.

- **Payload Sets**: Different payloads per position.
- **Payload Options**: Add, load, remove payloads.
- **Payload Processing**: Modify payloads (regex, prefix/suffix).
- **Payload Encoding**: Adjust encoding settings.

**Payload Configuration Examples:**

- Setting payload types and options:  
![Payloads Setup 1](https://github.com/user-attachments/assets/3e476dcd-5b87-47c0-929b-604759f22ee4)

- Managing payload encoding and processing:  
![Payloads Setup 2](https://github.com/user-attachments/assets/d9b1678c-de30-49da-91d7-40dd2b7ea167)

---

## 📌 Task 5: Attack Types Overview

Intruder has four attack types:

| Attack Type | Description                                                  |
|-------------|--------------------------------------------------------------|
| **Sniper**      | Tests each payload sequentially in each position.             |
| **Battering Ram** | Inserts the same payload simultaneously into all positions.   |
| **Pitchfork**    | Concurrently tests multiple payload lists per position.       |
| **Cluster Bomb** | Exhaustively tests all combinations across positions.         |

---

## 📌 Task 6: Sniper Attack

**Sniper** sequentially tests one position with a payload set.

**Example:**

Payloads: `admin`, `user`, `test`

| Request | Body                              |
|---------|-----------------------------------|
| 1       | `username=admin&password=12345`   |
| 2       | `username=user&password=12345`    |
| 3       | `username=test&password=12345`    |

Ideal for single-field brute-force testing.

---

## 📌 Task 7: Battering Ram Attack

**Battering Ram** simultaneously tests all positions with identical payloads.

**Example:**

Payloads: `admin`, `user`, `test`

| Request | Body                            |
|---------|---------------------------------|
| 1       | `username=admin&password=admin` |
| 2       | `username=user&password=user`   |
| 3       | `username=test&password=test`   |

Efficient for simultaneous payload injection.

---

## 📌 Task 8: Pitchfork Attack

**Pitchfork** concurrently tests multiple positions with separate payload lists.

**Example:**

- Usernames: `joel`, `harriet`  
- Passwords: `J03l`, `Emma1815`

| Request | Body                                 |
|---------|--------------------------------------|
| 1       | `username=joel&password=J03l`        |
| 2       | `username=harriet&password=Emma1815` |

Ideal for credential-stuffing.

---

## 📌 Task 9: Cluster Bomb Attack

**Cluster Bomb** exhaustively tests all combinations of payload sets.

**Example:**

- Usernames: `joel`, `harriet`  
- Passwords: `J03l`, `Emma1815`

| Request | Body                                 |
|---------|--------------------------------------|
| 1       | `username=joel&password=J03l`        |
| 2       | `username=joel&password=Emma1815`    |
| 3       | `username=harriet&password=J03l`     |
| 4       | `username=harriet&password=Emma1815` |

Perfect for exhaustive brute-force tests.

---

## 📌 Task 10: Practical Example - Credential Stuffing

Attack login: `http://MACHINE_IP/support/login`.

1. Capture and send login request to Intruder.
2. Set positions (username/password), attack type: **Pitchfork**.
3. Load username/password lists.
4. Launch and analyze responses for successful login by length.

---

## 📌 Task 11: Practical Challenge - IDOR Testing

Test potential IDOR vulnerability at:  
`http://MACHINE_IP/support/ticket/NUMBER`.

1. Capture a ticket request.
2. Fuzz numeric IDs using Sniper (1-100).
3. Review responses for unauthorized ticket access.

---

## 📌 Task 12: Advanced Credential Stuffing (Burp Macros)

Complex credential stuffing at:  
`http://MACHINE_IP/admin/login`.

We face dynamically generated tokens and session cookies.

**Step-by-Step Guide with Macros:**

1. **Capture initial login request:**  
   ![Macro Step 1](https://github.com/user-attachments/assets/79e06219-a6c7-4a1a-af40-8c148f62e7e7)

2. **Create a Burp Macro:**  
   ![Macro Step 2](https://tryhackme-images.s3.amazonaws.com/user-uploads/645b19f5d5848d004ab9c9e2/room-content/3b370cfce8a050faf415c7d9a5a8227e.gif)

3. **Configure Session Handling Rules:**  
   - Define session handling scope:  
     ![Macro Step 3](https://github.com/user-attachments/assets/f968ecb9-1078-451e-9d9d-11bc0900f111)
   - Configure macro actions and parameters:  
     ![Macro Step 4](https://github.com/user-attachments/assets/a6b9cff3-6a9d-45b8-9040-a85616b95623)
   - Limit macro actions to specific fields (`loginToken`, `session` cookie):  
     ![Macro Step 5](https://tryhackme-images.s3.amazonaws.com/user-uploads/645b19f5d5848d004ab9c9e2/room-content/250c140897e3b470093e7232c70c07cf.gif)

4. **Payload Setup:**  
   Use **Pitchfork** with username/password lists.

5. **Launch Attack:**  
   - Analyze results by response length (shortest length indicates successful login).

---

## 📌 Task 13: Conclusion

🎉 **Congratulations!** You now have comprehensive knowledge of Burp Suite's Intruder capabilities, including advanced techniques and macros for sophisticated attacks.

Continue exploring Burp Suite to enhance your security expertise!
