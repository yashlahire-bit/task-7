# task7-EL-
# Web Application Security & Penetration Testing Project

## 🛠 Tools Used
* **Target:** OWASP Juice Shop (Vulnerable Web App)
* **Proxy:** Burp Suite Community Edition
* **Environment:** Kali Linux / Docker

---

## 🔍 Vulnerabilities Tested

### 1. SQL Injection (SQLi)
* **Objective:** Bypass the login authentication to gain Administrative access.
* **Vulnerability:** The login form lacked input sanitization, allowing raw SQL commands to be executed.
* **Payload:** `' OR 1=1 --`
* **Result:** Successfully bypassed password authentication and logged into the `admin@juiceshop.op` account.



### 2. Cross-Site Scripting (XSS)
* **Objective:** Execute arbitrary JavaScript in the client-side browser.
* **Vulnerability:** The search functionality reflected user input back to the page without proper encoding.
* **Payload:** `<script>alert('XSS_Success')</script>`
* **Result:** Triggered a browser alert, proving the application is vulnerable to session hijacking and data theft.

### 3. Request Interception & Manipulation
* **Objective:** Manipulate data in transit to alter application logic.
* **Vulnerability:** Lack of server-side validation for pricing and quantity parameters.
* **Method:**
    1. Intercepted the `POST /api/BasketItems/` request using Burp Suite.
    2. Modified the `quantity` parameter from `1` to `-10`.
    3. Modified the `price` field to `0`.
* **Result:** Successfully added items to the basket with a negative total balance.



---

## 🛡 Mitigation Strategies

| Vulnerability | Remediation Recommendation |
| :--- | :--- |
| **SQL Injection** | Use **Prepared Statements** (Parameterized Queries) to separate data from code. |
| **XSS** | Implement **Context-aware Output Encoding** and a strong **Content Security Policy (CSP)**. |
| **Price Tampering** | Never trust client-side data; **re-validate all prices and totals on the server-side** before processing. |

---

## 🚀 How to Reproduce
1. Deploy Juice Shop via Docker: `docker run --rm -p 3000:3000 bkimminich/juice-shop`.
2. Configure Burp Suite to intercept traffic from your browser.
3. Apply the payloads documented in the "Vulnerabilities Tested" section above.

## ⚖️ Disclaimer
This project is for educational purposes only. Unauthorized testing of systems you do not own is illegal.
