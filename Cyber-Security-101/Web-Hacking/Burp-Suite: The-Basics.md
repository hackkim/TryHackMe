# 🔐 Burp Suite Basics (TryHackMe)

---

## 🛡️ Task 1: Introduction

![Burp Suite Logo](https://github.com/user-attachments/assets/345248ff-d124-44b0-9ec2-d224f56d42e9)

Welcome to **Burp Suite Basics**.  
This room provides an essential foundation for understanding Burp Suite:

- Introduction to Burp Suite
- Core components overview
- Installation on various platforms
- Configuration and initial navigation

Focus: **Theory first** — practical usage will come in future rooms.  
✅ **Best strategy**: Read carefully + actively experiment inside Burp.

---

## 🛡️ Task 2: What is Burp Suite


![Burp Proxy Intercept Example](https://github.com/user-attachments/assets/196ed497-3429-48eb-af5e-c4cb88cc2f68)
![Burp Enterprise Dashboard](https://github.com/user-attachments/assets/3cb44fb7-1675-4a8d-851a-02e410f00d4d)


Burp Suite is a **Java-based** framework for web application penetration testing.  
It captures, intercepts, modifies, and analyzes **HTTP/HTTPS traffic** between browser and server.

**Editions**:
- **Community**: Free basic version
- **Professional**: Advanced scanning, automation, API integrations
- **Enterprise**: Continuous automated scanning for enterprise apps

Focus of this room = **Community Edition** (free).

---

## 🛡️ Task 3: Features of Burp Community

Despite limitations, Burp Community is powerful.

Key tools:
- **Proxy**: Intercept HTTP/HTTPS traffic.
- **Repeater**: Manually resend customized requests.
- **Intruder**: Send multiple payloads for brute force/fuzzing (rate-limited).
- **Decoder**: Encode/decode payloads easily.
- **Comparer**: Compare two requests/responses.
- **Sequencer**: Analyze randomness (e.g., session tokens).

✅ Extensions via **BApp Store** (limited but valuable for Community users).

---

## 🛡️ Task 4: Installation


![Burp Suite Download Page](https://github.com/user-attachments/assets/85c14c20-e8a1-41fe-aa7c-28e860dbf34f)


- **Kali Linux**: Pre-installed.
- **Windows/macOS/Linux**: Download from [PortSwigger](https://portswigger.net/burp/releases).

**Linux Install** Example:
```bash
chmod +x BurpSuiteCommunity.sh
./BurpSuiteCommunity.sh
```

🛠️ Launch Burp after installation to configure.

---

## 🛡️ Task 5: The Dashboard


![Burp Suite Dashboard Sections](https://github.com/user-attachments/assets/9746924b-137b-4ced-acc5-d1fb77388a78)
![Burp Official Dashboard Documentation](https://github.com/user-attachments/assets/8a7c275d-e4c1-458e-ad93-29b22a499021)


Burp Dashboard shows:
- **Tasks**: Background passive crawls
- **Event Log**: Proxy events and actions
- **Issue Activity**: (Professional only — shows scan results)
- **Advisories**: Vulnerability explanations

Look for **?** icons everywhere for built-in help!

---

## 🛡️ Task 6: Navigation


![Burp Suite Module Tabs](https://github.com/user-attachments/assets/108c7bb4-2eb6-4535-a1b4-f4be722f127e)
![Window Detach Options](https://github.com/user-attachments/assets/8314dd83-f2f2-42c4-9298-18db1ae29bfa)


- Top menu bar switches between **modules** (Proxy, Repeater, etc.).
- Secondary menu for **sub-tabs** inside each module.

**Pro Tip**:  
Tabs can be **detached** into separate windows.

**Keyboard Shortcuts**:
- `Ctrl + Shift + D`: Dashboard
- `Ctrl + Shift + P`: Proxy
- `Ctrl + Shift + R`: Repeater

---

## 🛡️ Task 7: Options


![Burp Suite Settings Access](https://github.com/user-attachments/assets/ed235e00-6287-4e38-b034-41e82e1e8351)
![Proxy Listeners Settings](https://github.com/user-attachments/assets/63c391f9-d890-4fd3-ba70-36c21b91e668)
![Scope Settings](https://github.com/user-attachments/assets/453dc6d4-7647-42cf-a204-928ab9501543)
![Quick Access Proxy Settings](https://github.com/user-attachments/assets/a14aadc3-d45e-40c8-9304-37330bbc7629)


- **Global (User) Settings**: Persist across sessions.
- **Project Settings**: Temporary session settings.

Access:  
`Settings → Search or navigate categories`

Tools (e.g., Proxy) offer shortcuts to specific config pages.

---

## 🛡️ Task 8: Introduction to the Burp Proxy

![Burp Proxy Intercept Raw Request](https://github.com/user-attachments/assets/cdda6d5c-3755-4ecb-bdea-bd9635b8745b)
![Burp HTTP History Tab](https://github.com/user-attachments/assets/59a94027-79ff-4a77-86a0-441de1f65235)
![Burp Response Intercept Settings](https://github.com/user-attachments/assets/1abf243f-dd92-485b-8bde-33ac82518152)

**Proxy** = Capture and manipulate HTTP/HTTPS traffic.

Key behaviors:
- Requests intercepted by default
- Logs HTTP requests/responses
- Support for WebSocket traffic

💬 Modify requests on-the-fly or replay them using Repeater.

Proxy Settings Highlights:
- **Match and Replace**: Auto-modify headers/payloads.
- **Intercept Responses**: Optionally intercept server responses too.

---

## 🛡️ Task 9: Connecting through the Proxy (FoxyProxy)


![FoxyProxy Extension Icon](https://github.com/user-attachments/assets/f6ecdaf4-a944-4951-9539-a303546bacbc)
![FoxyProxy Options Add Proxy](https://github.com/user-attachments/assets/7cda84ad-ecae-4f7e-958b-8b4ecfd48429)
![FoxyProxy Configure Proxy Settings](https://github.com/user-attachments/assets/459bd9a9-4ab1-4661-b598-37a3f3a7a3d3)
![FoxyProxy Proxy Active](https://github.com/user-attachments/assets/eb154e0f-35ce-496e-8300-a9a4f75bd5f8)
![Burp Proxy Intercept Active](https://github.com/user-attachments/assets/c625f3aa-2725-45f3-aa28-f5606507c77d)


Steps:
1. Install **FoxyProxy** extension on Firefox.
2. Configure new proxy:
   - IP: `127.0.0.1`
   - Port: `8080`
3. Enable Intercept in Burp Proxy.
4. Visit a site — see the intercepted HTTP request!

✅ Critical first step to integrate browser traffic into Burp.

---

## 🛡️ Task 10: Site Map and Issue Definitions

- **Site Map**: Automatic tree-view of visited endpoints.
- **Issue Definitions**: List of web vulnerabilities (informational only in Community Edition).
- **Scope Settings**: Define what is in-scope/out-of-scope for testing.

**Pro Tip**: Site Map = perfect for API enumeration too.

---

## 🛡️ Task 11: The Burp Suite Browser


![Burp Suite Open Browser Button](https://github.com/user-attachments/assets/07eef31f-bae0-48b8-9d20-10b2a0e97777)


Burp provides its own built-in **Chromium Browser**:

- Pre-configured to use Burp Proxy
- No manual proxy setup required

**Linux Root User Tip**:
If browser won't launch:
- Go to `Settings → Tools → Burp's Browser`
- Enable "Allow browser to run without sandbox"

---

## 🛡️ Task 12: Scoping and Targeting

![Burp Scope Right-Click Menu](https://tryhackme-images.s3.amazonaws.com/user-uploads/645b19f5d5848d004ab9c9e2/room-content/5db0a2b0597830ae32aaaf9b80d73187.gif)
![Burp Intercept Only In Scope](https://github.com/user-attachments/assets/1fecf5c6-4ee9-414b-a9ab-91d753f42007)

Set scope to:
- Focus on **in-scope traffic only**
- Ignore unnecessary noise

Steps:
1. Right-click domain in Target → Add To Scope
2. Proxy → Intercept Client Requests → Enable "Only if URL is in scope"

✅ Result: Cleaner captures, easier testing.

---

## 🛡️ Task 13: Proxying HTTPS


![Firefox Certificate Error Warning](https://github.com/user-attachments/assets/4b2720be-a947-44dc-b21b-202e41421b0e)
![Firefox Certificate Settings Search](https://github.com/user-attachments/assets/2e823932-eea5-4825-96d2-659f6ac986d6)
![Trust PortSwigger CA Certificate](https://github.com/user-attachments/assets/989c7ac1-94b1-4577-986c-0d2d09c259cf)
![Firefox Certificate Manager](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d9e176315f8850e719252ed/room-content/fb2a8717ae887eda024a7791d83cefaf.gif)


Issue: HTTPS sites show security error because Burp uses a self-signed CA certificate.

Fix:
1. Visit `http://burp/cert`
2. Download `cacert.der`
3. In Firefox:
   - `about:preferences`
   - View Certificates → Import → Select `cacert.der`
   - Trust the CA

✅ Now HTTPS interception works seamlessly!

---

## 🛡️ Task 14: Example Attack - Reflected XSS


![Support Form Input](https://github.com/user-attachments/assets/461e4c0b-6c25-43fb-891e-412661fc7fb0)
![Support Form Typing](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d9e176315f8850e719252ed/room-content/04acd78be44400cf105c7d41b104b7fe.gif)
![Intercepted Support Form Submission](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d9e176315f8850e719252ed/room-content/58c5bf5382cdee55ab12e0752d819ebe.gif)
![Successful XSS Popup](https://github.com/user-attachments/assets/cb628736-3ab7-4721-8bb9-3fc759b719e8)


Walkthrough:
1. Submit normal support ticket.
2. Intercept in Proxy.
3. Modify email field to payload:
```html
<script>alert("Succ3ssful XSS")</script>
```
4. URL encode payload.
5. Forward the request.

Result ➔ Alert box pops up confirming successful XSS!

---

## 🛡️ Task 15: Conclusion

🎉 Congratulations! You now know:

- Burp Suite installation & setup
- Proxy configuration
- Traffic interception basics
- Using Site Map, Scope, and browser integration
- Executing basic manual attacks (like XSS)

🚀 **Next up**: Mastering Burp Suite Repeater for advanced manual testing!

Keep practicing, stay curious, and enjoy hacking! 🔥

---
