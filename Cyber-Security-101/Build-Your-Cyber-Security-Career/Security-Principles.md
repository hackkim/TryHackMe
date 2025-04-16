# 🔐 TryHackMe: Security Principles

> Comprehensive summary of the **Security Principles** room from TryHackMe, detailing foundational security concepts, principles, and models.

---

## 📌 Task 1: Introduction

![Task 1 Illustration](https://github.com/user-attachments/assets/8282f8b2-f167-4239-bf8b-9358d7dad9c9)

Security is increasingly critical as more organizations claim their products or services are secure. However, security is context-dependent; understanding the adversary is crucial. Protection against trivial threats (e.g., a child accessing a laptop) is fundamentally different from protecting against professional threats such as industrial espionage.

### Objectives:
- Explain fundamental security principles: **Confidentiality, Integrity, Availability (CIA)**.
- Introduce the inverse **Disclosure, Alteration, Destruction (DAD)** triad.
- Discuss core security models (Bell-LaPadula, Biba, Clark-Wilson).
- Explain principles: **Defence-in-Depth, Zero Trust, Trust but Verify**.
- Introduce the ISO/IEC 19249 standard.
- Clarify differences among **Vulnerability, Threat, and Risk**.

---

## 🔑 Task 2: CIA Triad

![CIA Triad Illustration](https://github.com/user-attachments/assets/4e7dd204-69ee-4999-81b7-f28d1e4fc2f8)

Security is defined primarily by the CIA triad:

- **Confidentiality**: Ensures data access only to authorized individuals.
- **Integrity**: Data must remain accurate and unaltered.
- **Availability**: Data/services must be reliably accessible.

### Real-world Examples:

#### Online Shopping:
![Integrity Illustration](https://github.com/user-attachments/assets/12dee2ac-6fa1-401c-9e0b-2b950b79bab2)
- **Confidentiality**: Credit card information should remain private.
- **Integrity**: Shipping address must not be altered.
- **Availability**: The online store should always be accessible.

#### Medical Records:
- **Confidentiality**: Medical records must be protected due to legal obligations.
- **Integrity**: Any unauthorized alteration can cause severe harm.
- **Availability**: Essential for timely medical diagnosis and treatment.

### Additional Concepts:
![Nonrepudiation Illustration](https://github.com/user-attachments/assets/a913b04a-0ad2-43fc-9421-7e3947c93d5c)
- **Authenticity**: Verifying the source is legitimate.
- **Nonrepudiation**: Preventing denial of actions taken.

### Parkerian Hexad:
Expanding beyond CIA:
1. Availability
2. Utility (Information usefulness)
3. Integrity
4. Authenticity
5. Confidentiality
6. Possession (Preventing unauthorized control of data)

---

## 🚨 Task 3: DAD Triad

![DAD Triad Illustration](https://github.com/user-attachments/assets/817941b7-4412-4b18-80d3-ac91046e8912)

Opposite of CIA:
- **Disclosure** (Opposite of Confidentiality)
- **Alteration** (Opposite of Integrity)
- **Destruction/Denial** (Opposite of Availability)

### Example in Healthcare:
- **Disclosure**: Unauthorized data leak.
- **Alteration**: Modification of patient records.
- **Destruction/Denial**: Data unavailable due to cyberattack.

Security requires a balanced approach; overemphasizing one aspect can negatively impact others.

---

## 📚 Task 4: Fundamental Security Models

### Bell-LaPadula Model (Confidentiality)
- **Simple Security Property (No Read-Up)**: Lower clearance users cannot read higher-level data.
- **Star Security Property (No Write-Down)**: Higher clearance users cannot write data to lower-level users.
- **Discretionary Security Property**: Uses access matrices for controlled access.

### Biba Model (Integrity)
- **Simple Integrity Property (No Read-Down)**: Higher integrity users cannot read lower integrity data.
- **Star Integrity Property (No Write-Up)**: Lower integrity users cannot write to higher integrity data.

### Clark-Wilson Model (Integrity)
- **Constrained Data Items (CDI)**: Sensitive data needing protection.
- **Unconstrained Data Items (UDI)**: Data inputs.
- **Transformation Procedures (TPs)**: Operations ensuring CDI integrity.
- **Integrity Verification Procedures (IVPs)**: Validate CDI integrity.

---

## 🛡️ Task 5: Defence-in-Depth

![Defence-in-Depth Illustration](https://github.com/user-attachments/assets/61187214-df44-4c11-9e23-bc591e0bd474)

Defence-in-Depth (Multi-Level Security) involves layered protection:
- Example: Locked drawer → locked room → locked apartment → locked building → CCTV.
- Reduces risk significantly by adding multiple security layers.

---

## 🌎 Task 6: ISO/IEC 19249

ISO/IEC 19249 provides guidelines for secure system and application design.

### Architectural Principles:
- Domain Separation
- Layering
- Encapsulation
- Redundancy
- Virtualization

### Design Principles:
- Least Privilege
- Attack Surface Minimization
- Centralized Parameter Validation
- Centralized Security Services
- Error and Exception Handling

---

## 🔍 Task 7: Zero Trust vs. Trust but Verify

- **Trust but Verify**: Even trusted entities should be monitored through logs and audits.
- **Zero Trust**: Never trust implicitly; always verify. Every entity is considered potentially harmful until validated.

---

## ⚠️ Task 8: Threat vs. Risk

![Threat vs. Risk Illustration](https://github.com/user-attachments/assets/713236ab-695c-43bd-baa5-0ac1a0bdaf74)

- **Vulnerability**: System weakness susceptible to attacks.
- **Threat**: Potential actor/action exploiting vulnerabilities.
- **Risk**: Probability and impact of a threat exploiting vulnerabilities.

### Example:
- Vulnerability: Unpatched medical records database.
- Threat: Exploit available publicly.
- Risk: High likelihood of records compromise or data loss.

---

## 🎯 Task 9: Conclusion

Key Takeaways:
- Mastery of CIA and DAD security concepts.
- Understanding core security models (Bell-LaPadula, Biba, Clark-Wilson).
- Knowledge of Defence-in-Depth, Zero Trust, Trust but Verify.
- Familiarity with ISO/IEC 19249 standard principles.
- Clear differentiation between Vulnerabilities, Threats, and Risks.

### Additional Concepts:
- **Shared Responsibility Model** in cloud environments: Security shared between cloud providers and users (e.g., SaaS vs. IaaS).

✅ **Next Steps**: Proceed to **Intro to Cryptography** for exploring data encryption methods and principles.

