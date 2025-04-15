# 🍳 TryHackMe - CyberChef: The Basics

> CyberChef is a powerful web-based tool developed by GCHQ for performing data transformations, decodings, and extractions.  
> It simplifies complex encoding tasks through an intuitive drag-and-drop interface using “recipes.”

---

## 🧠 Task 1 - Introduction

![CyberChef Recipe Pipeline](https://github.com/user-attachments/assets/477fb27b-9bb4-4061-956c-f3555e0e1f7d)

CyberChef is often referred to as the **Swiss Army knife of cybersecurity** because it provides a rich set of functionalities for data analysis, transformation, and encoding/decoding.

### 🔧 What CyberChef Can Do

- Encoding & decoding: Base64, Base32, Base58, Base85, Hex, ROT13, etc.
- Hashing: MD5, SHA1, SHA256, SHA512, etc.
- Extractors: IPs, emails, URLs
- Encryption: AES, DES, RSA (public key decryption)
- Parsing: JWT, IPv4 headers, timestamps
- Analysis: XOR brute force, entropy, frequency

---

## 🎯 Learning Objectives

- Understand CyberChef’s capabilities and structure
- Learn how to navigate its interface
- Use recipes to automate multiple transformations
- Recognize common operation categories

---

## 🌍 Task 2 - Accessing the Tool

### 🖥️ Online Use

Access CyberChef directly:
- **Web URL**: [https://gchq.github.io/CyberChef](https://gchq.github.io/CyberChef)
- No installation or account required

### 🗂️ Offline Use

You can run CyberChef locally:
- Go to: [CyberChef GitHub Releases](https://github.com/gchq/CyberChef/releases)
- Download the latest `.html` file
- Open it in your browser (supports Windows, Linux, macOS)

---

## 🧭 Task 3 - Navigating the Interface


![CyberChef Interface Overview](https://github.com/user-attachments/assets/3f5e9f33-0531-4e83-bc0b-0d81c5cee46d)

![Operation Hover Description](https://github.com/user-attachments/assets/6a05bd29-5306-49e8-a57e-b86078ebe1fc)

![Recipe Save/Load/Clear](https://github.com/user-attachments/assets/eae71f6e-fc56-4c65-8076-dc7e3eff15d6)

![Input Panel Options](https://github.com/user-attachments/assets/8577c6d7-c0c5-4913-b1f8-7d836c4d0c84)

![Multiple Input Tabs](https://github.com/user-attachments/assets/82684199-5ef0-47fb-a4ed-a08ffda7a175)

![Open Folder as Input](https://github.com/user-attachments/assets/eba5f3f1-8a94-4feb-b3e3-cfeba12f90c2)

![Open File as Input](https://github.com/user-attachments/assets/1e0aa587-4ff9-41e6-9d93-b19d25a08a52)

![Output Panel Options](https://github.com/user-attachments/assets/b4d87ac3-0cbf-4f4a-b67f-251f1641a059)


CyberChef’s GUI consists of four main panels:

### 🔹 1. Operations Panel
- Lists all available operations (categorized)
- Search functionality to find operations quickly
- Hovering over each operation gives:
  - Description
  - Example input/output
  - Links to documentation

### 🧪 Common Operations

| Operation         | Description                                                | Example Input      | Output                     |
|------------------|------------------------------------------------------------|--------------------|----------------------------|
| From Base64      | Decodes Base64 string                                      | `VEhN`             | `THM`                      |
| URL Decode       | Converts percent-encoded URI back to raw characters        | `%2F%2Ftryhackme`  | `//tryhackme`              |
| To Hex           | Converts to hex values separated by delimiters             | `THM`              | `54 48 4D`                 |
| ROT13            | Applies Caesar cipher with rotation                        | `CyberChef`        | `PlorePurc`                |
| Extract IPs      | Extracts IPv4/IPv6 addresses                               | Raw text           | `10.10.10.10`              |
| Extract Emails   | Finds email formats                                        | Text w/ `@` symbols| `user@example.com`         |

---

### 🔹 2. Recipe Panel (Center)

The **Recipe Panel** is where you:
- Drag operations into the sequence
- Configure arguments for each operation
- Reorder or delete steps
- Use:
  - **Save Recipe** / **Load Recipe**
  - **Clear Recipe**
  - **Auto Bake / Manual Bake**

> Think of this area as your operation automation pipeline.

---

### 🔹 3. Input Panel

- You can paste text, upload files, or open folders
- Supports:
  - New input tabs
  - Clear input
  - Reset panel layout

> Ideal for testing multiple strings, files, or log fragments

---

### 🔹 4. Output Panel

Displays the transformed or decoded output.

Key features:
- **Copy to clipboard**
- **Save to file**
- **Replace input with output**
- **Maximize output panel**

---

## 🔍 Task 4 - Before Anything Else


![CyberChef Thought Process](https://github.com/user-attachments/assets/20f57997-e1de-4065-952e-83770bc7dd62)

![CyberChef Example Process](https://github.com/user-attachments/assets/794b7544-5273-46db-aaa4-46c8da977603)


### 🔄 CyberChef Analysis Workflow

1. **Define the Objective**
   - _e.g., Decode obfuscated Base64 payload in phishing email_

2. **Paste or Load Input**
   - Drag/drop file or string

3. **Build Recipe**
   - Add operations (e.g., From Base64 → Extract Email → URL Decode)

4. **Review Output**
   - Did it match your goal?
   - If not, iterate steps 2–3

---

## 🧪 Task 5 - Practical Operation Categories

### 📦 Extractors

| Operation              | Description                        |
|------------------------|------------------------------------|
| Extract IP addresses   | Finds all valid IPv4/IPv6          |
| Extract email addresses| Finds strings matching `*@*.*`     |
| Extract URLs           | Locates HTTP, HTTPS, FTP links     |

---

### 🕒 Date / Time

| Operation             | Description                         |
|-----------------------|-------------------------------------|
| From UNIX Timestamp   | Converts epoch to readable date     |
| To UNIX Timestamp     | Converts human date to UNIX         |

---

### 🔠 Encoding / Decoding

| Operation       | Description                                | Example             |
|-----------------|--------------------------------------------|---------------------|
| From Base64     | Converts `VEhN` → `THM`                    | `VEhN` → `THM`      |
| From Base85     | Converts base85 encoded text               | `BOu!rD]j7` → hello |
| URL Decode      | `%3A%2F` → `:/`                            |                     |

---

### 📈 Base64 Manual Explanation (Advanced Learning)

Steps to convert "THM" → `VEhN`:
- Convert to binary
- Chunk into 6-bit sections
- Translate into Base64 index
- Output mapped chars from table

> This gives you a deep understanding of **encoding math**, not just CyberChef usage.

---

## 👨‍🍳 Task 6 - Your First Official Cook

![Your Turn to Cook](https://github.com/user-attachments/assets/d636dfcc-1325-4400-9d4c-8e174841697b)

Apply CyberChef to decode, extract, or analyze real inputs.

Instructions:
- Download provided task files
- Use drag-and-drop operations
- Focus on `Extractors`, `Encoding`, and `Date/Time`
- Try solving without hints

🎯 Goal: Combine theory + tool skill in one interactive session

---

## ✅ Task 7 - Conclusion

CyberChef is a **must-have tool** for cybersecurity professionals. It bridges data processing, decoding, and transformation **without writing code**.

You’ve learned:
- Core interface elements
- How to design and execute recipes
- Popular use cases: Base64, URL decoding, timestamps
- Deeper insight into encoding methods

---

## 🚀 Pro Tips

- Bookmark useful recipes
- Try chaining obscure operations (XOR, GZIP, Base85)
- Integrate with other tools like:
  - Burp Suite
  - REMnux
  - Ghidra (via preprocessing)

---

## 📚 Further Reading

- [CyberChef Documentation](https://gchq.github.io/CyberChef/)
- [CyberChef GitHub Repo](https://github.com/gchq/CyberChef)
