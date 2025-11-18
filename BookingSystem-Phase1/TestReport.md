# 1️⃣ Introduction

**Tester(s):**  
- Name:  Markku Niemi

**Purpose:**  
- The purpose of this penetration test was to evaluate security, privacy and reliability of the given Booking System's registration functionality. Main purpose was to get familiar with penetration testing in web application and with different kind of approaches. Also the goal was to identify vulnerabilities, anomalies and weaknesses when creating new accounts.

**Scope:**  
- Tested components:
  - Registration page
  - All input fields (email, password, birthdate, role)
  - Client-side behaviour (form validation, error messages)
  - Server responses (status codes, 500 errors)
  - Database behaviour (inserts, malformed data, constraint errors)
  - Docker container logs (web + database)
  - Automated scanning results (ZAP, 3 scans)
    
- Exclusions:
  - Login functionality
  - Reservation features
  - Administrator interface
  - Authorisation logic beoynd registration
  - Performance testing / load testing
  - DoS attack
    
- Test approach:
  - Gray-box

**Test environment & dates:**  
- Start:  15.11.2025
- End:  17.11.2025
- Test environment details (OS, runtime, DB, browsers):
  - OS: Debian 12 (VirtualBox, VM)
  - Host system: Windows 11
  - Container Runtime: Docker Engine 26.x + Docker Compose v2
  - Database: PostgreSQL 15 (in Docker container)
  - Web Application: Booking System Phase 1 (Docker)
  - Browser: Firefox (Debian) + Chrome (Windows via port forwarding)
  - Tools: ZAP 2.16.1, browser DevTools, Docker logs, PostgreSQL CLI

**Assumptions & constraints:**  
- No user credentials werw provided
- Only the registration functionality was in scope
- All tests were performed in a local isolated lab environment (VirtualBox + Docker)
- Source code was not available. testing relied on gray-box techniques (DevTools, DB access, logs)
- No denial-of-service or destructive testing was performed
- External services, login flow and reservation logic were excluded from this phase

---

# 2️⃣ Executive Summary

**Short summary (1-2 sentences):**  
Booking System's registration functionality was tested with manual methods and with automated ZAP scanning. Several security issues, including unauthorized role choices and plaintext password storage, along with several input validation issues and error-handling problems were found rangign from high to low.

**Overall risk level:** (Low / Medium / High / Critical)
- High

**Top 5 immediate actions:**  
1.  Remove ability to choose the role of the user in registration sheet. This should be handled from backend.
2.  Add proper password hashing and avoid storing any credentials in plaintesxt.
3.  Add backend validation for all form inputs (email. password strength, birthdate checking to make sure user is atleast 15yr)
4.  Fix error handling to avoid 500 Internal Server Errors and avoid leaking database information.
5.  Add security headers (CSP,X-Frame-Options, X-Content-Type-Options).

---

# 3️⃣ Severity scale & definitions

|  **Severity Level**  | **Description**                                                                                                              | **Recommended Action**           |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
|      🔴 **High**     | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | *Immediate fix required*         |
|     🟠 **Medium**    | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF).                              | *Fix ASAP*                       |
|      🟡 **Low**      | A minor issue or configuration weakness (e.g., server version disclosure).                                                   | *Fix soon*                       |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers).                                            | *Monitor and fix in maintenance* |


---

# 4️⃣ Findings (filled with examples → replace)

> Fill in one row per finding. Focus on clarity and the most important issues.

| ID | Severity | Finding | Description | Evidence / Proof |
|------|-----------|----------|--------------|------------------|
| F-01 | 🔴 High | Unauthorized admin role creation | Registration allows user to create "Administrator" account without backend validation enabling privilege escalation during account creation. | Screenshot <img width="1277" height="809" alt="SQL" src="https://github.com/user-attachments/assets/346b6262-14e8-4037-8485-9f10fc3c649b" />|
| F-02 | 🔴 High  | Passwords stored in plaintext | All passwords are sre stored in plaintext in database. There should be some kind of hashing or encryption ude. Exposing credentials directly | See screenshot in F-01 |
| F-03 | 🟠 Medium | Missing age verification | There is no birthdate verification. Users below age 15 can register to the web software | See screenshot in F-01 |
| F-04 | 🟠 Medium | 500 Internal Server Error reveals database detalis | Invalid or unexpected input (e.g., missing or modified role value) causes the backend to crash with a 500 Internal Server Error. The error message exposes internal database structure, including table names and constraint names (booking_users_role_check, booking_users_username_key). This information disclosure widens the attack surface and indicates missing backend validation and insufficient error handling. | Screenshots  <img width="1275" height="809" alt="Erroreita1" src="https://github.com/user-attachments/assets/6671189b-c5a9-431d-b567-b46ee7d55252" /> <img width="1277" height="809" alt="Erroreita2" src="https://github.com/user-attachments/assets/2389b1c3-ef4e-438f-bc8d-8596304e685d" />|
| F-05 | 🟡 Low | Missing security headers | No CSP, X-Frame-Options or X-Content-Type-Options headers are present, reducing baseline protection against clickjacking and content-type attacks. | See the ZAP report |

---

> [!NOTE]
> Include up to 5 findings total.   
> Keep each description short and clear.

---

# 5️⃣ OWASP ZAP Test Report (Attachment)

**Purpose:**  
- Attach or link your OWASP ZAP scan results (Markdown format preferred).

---

**Instructions (CMD version):**
1. Run OWASP ZAP baseline scan:  
   ```bash
   zap-baseline.py -t https://example.com -r zap_report_round1.html -J zap_report.json
   ```
2. Export results to markdown:  
   ```bash
   zap-cli report -o zap_report_round1.md -f markdown
   ```
3. Save the report as `zap_report_round1.md` and link it below.

---
> [!NOTE]
> 📁 **Attach full report:** → `check itslearning` → **Add a link here**
  - ZAP report link: [OWASP ZAP Report](./zap_report_round1.md)

---
