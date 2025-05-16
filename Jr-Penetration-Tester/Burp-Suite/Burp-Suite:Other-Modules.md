# 🔥 Burp Suite: Other Modules

This document covers Burp Suite's other powerful modules: **Decoder, Comparer, Sequencer, and Organizer**.

---

## ✅ Task 1: Introduction

Burp Suite includes several useful modules beyond Proxy, Repeater, and Intruder:

- **Decoder**: Encode and decode data.
- **Comparer**: Compare two sets of data.
- **Sequencer**: Analyze token entropy.
- **Organizer**: Store and annotate HTTP requests.

---

## ✅ Task 2: Decoder Overview

The Decoder module allows data encoding, decoding, and hashing operations efficiently.

**Image 1: Decoder Main Interface**  
![](https://github.com/user-attachments/assets/01999d85-00d3-49b2-bb97-d77a7fdac2d6)

**Image 2: Input selection (Text / Hex)**  
![](https://github.com/user-attachments/assets/2cc68390-dbb2-4fc8-9fdb-a3dabf470b19)

**Image 3: Encoder, Decoder, and Hash dropdown menu**  
![](https://github.com/user-attachments/assets/15a0fda5-d6bd-4f7d-a57c-0ff596b574f6)

---

## ✅ Task 3: Using Decoder (Encoding/Decoding)

Decoder supports various encoding/decoding methods:

- **URL Encoding/Decoding**
- **HTML Entities Encoding/Decoding**
- **Base64 Encoding/Decoding**
- **ASCII Hex Encoding/Decoding**
- **Hex, Octal, Binary conversions**
- **Gzip compression/decompression**
- **Smart Decode (automatic decoding)**

**Image 1: URL Encoding example**  
![](https://github.com/user-attachments/assets/0a40e974-0837-4c44-807a-e3cc74eba018)

**Image 2: HTML Entities Encoding example**  
![](https://github.com/user-attachments/assets/a270dcb4-9e9d-4733-a5ee-d652dc7df04d)

**Image 3: Base64 Encoding example**  
![](https://github.com/user-attachments/assets/4e8fa67e-f423-4c62-a870-9a927d2a314c)

**Image 4: ASCII Hex Encoding example**  
![](https://github.com/user-attachments/assets/c5952fee-4fab-4366-827a-a97b9bfcc15c)

**Image 5: Hex, Octal, Binary conversion example**  
![](https://github.com/user-attachments/assets/0bbcc030-305b-449f-aae5-73b5be6e0b30)

**Image 6: Gzip Encoding example**  
![](https://github.com/user-attachments/assets/60d5e1ac-e484-48c6-ac75-fb6dcde2493a)

**Image 7: Smart Decode example**  
![](https://github.com/user-attachments/assets/e663082f-a8a0-4705-bb52-1fa3e98dc6d2)

---

## ✅ Task 4: Hashing with Decoder

Decoder allows easy generation of hash values from data:

- Supports MD5, SHA-1, SHA-256, and more.
- Used for data integrity verification and secure password storage.

**Image 1: Hash dropdown menu**  
![](https://github.com/user-attachments/assets/9ee0b660-5ff6-412b-a3a9-9fe2da097890)

**Image 2: MD5 Hash generation example**  
![](https://github.com/user-attachments/assets/84154063-542d-4b87-867a-38ca8c4c5c50)

**Image 3: Converting Hash result to Hex example**  
![](https://github.com/user-attachments/assets/9c5ed97f-baab-4c55-8a64-268ff0c99b0f)

---

## ✅ Task 5: Comparer Overview

Comparer allows easy comparison between two datasets.

**Image 1: Comparer Main Interface**  
![](https://github.com/user-attachments/assets/f243f91c-ae2a-44df-914e-1ccca817f23d)

**Image 2: Comparer Result (highlighted differences)**  
![](https://github.com/user-attachments/assets/29cb1bfb-8585-4852-a766-8727a69fe603)

---

## ✅ Task 6: Comparer Practical Example

Using Comparer to identify differences between successful and failed login responses.

**Image 1: Login response comparison example**  
![](https://github.com/user-attachments/assets/94ad2874-bc62-4a14-8118-de30856c5246)

---

## ✅ Task 7: Sequencer Overview

Sequencer analyzes token randomness to evaluate their security (entropy analysis).

**Image 1: Sequencer Main Interface**  
![](https://github.com/user-attachments/assets/dd2b0139-4193-4871-bda5-b5e1c40cdf69)

---

## ✅ Task 8: Sequencer Live Capture Example

Using Sequencer's live capture feature to collect and analyze tokens:

**Image 1: Live Capture settings screen (token selection example)**  
![](<img width="605" alt="스크린샷 2025-05-16 오후 8 04 51" src="https://github.com/user-attachments/assets/6f7df539-ad4a-4c7c-885d-97417b080284" />
)

**Image 2: Live Capture running and Analysis button screen**  
![](https://github.com/user-attachments/assets/d2fe0e3f-c31c-45dd-b12a-4b411ab791cc)

---

## ✅ Task 9: Sequencer Analysis Results

Understanding the key results from Sequencer’s entropy analysis report.

**Image 1: Sequencer entropy analysis report**  
![](https://github.com/user-attachments/assets/b1e143b7-b604-4525-853d-36f740b3c1a4)

---

## ✅ Task 10: Organizer Overview

Organizer allows efficient management and annotation of HTTP requests.

**Image 1: Organizer Main Interface**  
![](https://github.com/user-attachments/assets/14db3ae2-140e-4b0b-ad3d-d1e183f369da)

**Image 2: Organizer Request List and Management options**  
![](https://github.com/user-attachments/assets/b8556fb1-2c71-4d67-9619-f5fe2e30a2ee)

**Image 3: Detailed Request View and Adding Annotations**  
![](https://github.com/user-attachments/assets/b070be3a-452f-4fd3-92bd-b790fb101431)

---

## ✅ Task 11: Conclusion

You now have a comprehensive understanding of Decoder, Comparer, Sequencer, and Organizer modules.

In the next room, explore **Burp Suite Extensions** for even greater capabilities!

---

🚀 **Happy Hacking!** 🚀
