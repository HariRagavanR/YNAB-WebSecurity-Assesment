# 🛡️ Web Application Security Assessment – YNAB (Staging)

## 📌 Overview

This repository documents a **legal, scope-restricted web application security assessment** performed on **YNAB (You Need A Budget)** staging environments as part of my **hands-on Web Pentesting learning journey**.

The objective of this assessment was **not bug hunting for rewards**, but to **practice real-world pentesting methodology**, including reconnaissance, traffic analysis, authentication logic testing, API access control verification, and professional documentation.

---
<img width="1920" height="1080" alt="Screenshot at 2026-01-01 20-49-32" src="https://github.com/user-attachments/assets/fd667233-f01d-499d-bb74-8dcc086e2fc5" />
<img width="1920" height="1080" alt="Screenshot at 2026-01-01 21-22-06" src="https://github.com/user-attachments/assets/29d2db30-0b1f-4876-9a2a-3db02f827a70" />
<img width="1920" height="1080" alt="Screenshot at 2026-01-01 21-22-18" src="https://github.com/user-attachments/assets/1169e03d-30b0-4ae1-bcfb-144cb1e85c49" />
<img width="1920" height="1080" alt="Screenshot at 2026-01-01 21-24-32" src="https://github.com/user-attachments/assets/3a5dc71d-0639-41bc-8b5d-252213c1614f" />
<img width="1920" height="1080" alt="Screenshot at 2026-01-01 21-25-03" src="https://github.com/user-attachments/assets/15d893a9-9061-44f4-a90c-6b9d5cfca64c" />

## 🎯 Scope & Authorization

All testing was conducted **strictly within the official Bugcrowd program scope**.

### ✅ In-Scope Targets

* `https://staging-www.ynab.com`
* `https://staging-api.bany.dev`
* Any other `*.ynab.com` hosts explicitly listed as in-scope

### 🚫 Out of Scope

* Production environment (`https://app.ynab.com`)
* Real user accounts or customer data
* Mobile applications
* Third-party hosted sites (support, learn, etc.)

> ⚠️ No automated exploitation, brute-force attacks, or scope violations were performed.

---

## 🧰 Tools Used

| Category                | Tools                |
| ----------------------- | -------------------- |
| Reconnaissance          | Subfinder, httpx     |
| Interception & Analysis | Burp Suite Community |
| Manual Testing          | Burp Repeater        |
| Documentation           | Markdown, GitHub     |

---

## 🧭 Methodology Followed

### 1️⃣ Reconnaissance

* Enumerated subdomains using **Subfinder**
* Identified live hosts using **httpx**
* Filtered in-scope assets only

```bash
subfinder -d ynab.com -silent | httpx -silent
```

---

### 2️⃣ Traffic Analysis

* Used Burp Suite Proxy to capture application traffic
* Filtered browser and OS noise (Mozilla telemetry, extensions, CDN traffic)
* Focused only on YNAB-owned endpoints

Key observation:

> Differentiating real application traffic from background browser noise is critical in real pentests.

---

### 3️⃣ Authentication Flow Testing

* Identified login endpoints (`/users/sign_in`)
* Tested invalid credential handling
* Verified consistent error responses
* Confirmed no username enumeration or logic bypass

Result:

* ✅ Authentication logic correctly enforced
* ❌ No bypass identified

---

### 4️⃣ Redirect & Flow Validation

Tested parameters such as:

* `redirect`
* `returnUrl`
* `state`

Payload examples:

```
redirect=/admin
redirect=//evil.com
redirect=../admin
```

Result:

* ✅ Redirects properly validated
* ❌ No open redirect vulnerabilities found

---

### 5️⃣ API Access Control Verification

* Observed API calls from the SPA
* Replayed requests without authorization tokens
* Tested unauthenticated API access

Result:

* ✅ API endpoints correctly returned `401 Unauthorized`
* ❌ No IDOR or privilege escalation observed

---

### 6️⃣ Parameter Tampering (Safe Testing)

* Tested non-sensitive parameters (analytics, flow params)
* No trust placed on client-side parameters by backend

Result:

* ✅ Secure server-side validation

---

## 📄 Findings Summary

| Category          | Result |
| ----------------- | ------ |
| Authentication    | Secure |
| Access Control    | Secure |
| Redirect Handling | Secure |
| API Authorization | Secure |
| Parameter Trust   | Secure |

> No exploitable vulnerabilities were identified within scope.

---

## 🧠 Key Learnings

* Real-world pentesting involves **extensive observation**, not just exploitation
* Most professional engagements result in **secure findings**
* Knowing **when to stop testing** is as important as finding bugs
* Proper scoping and documentation are essential skills for junior pentesters

---

## 📎 Disclaimer

This assessment was performed **solely for educational purposes** on **authorized, in-scope targets**.
No customer data was accessed, modified, or exposed.

---

## 👤 Author

**Hari Ragavendiran R**
Aspiring **Junior Web Application Pentester / VAPT Analyst**
Date: 01-01-2026
