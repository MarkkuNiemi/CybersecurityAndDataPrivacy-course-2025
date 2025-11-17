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
    
- Test approach: Gray-box

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
***KESKEN******KESKEN******KESKEN******KESKEN******KESKEN******KESKEN******KESKEN******KESKEN******KESKEN******KESKEN******KESKEN******KESKEN******KESKEN***
# 2️⃣ Executive Summary

**Short summary (1-2 sentences):**  

**Overall risk level:** (Low / Medium / High / Critical)

**Top 5 immediate actions:**  
1.  
2.  
3.  
4.  
5.  

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
| F-01 | 🔴 High | SQL Injection in registration | Input field allows `' OR '1'='1` injection | Screenshot or sqlmap result |
| F-02 | 🟠 Medium | Session fixation | Session ID remains unchanged after login | Burp log or response headers |
| F-03 | 🟡 Low | Weak password policy | Accepts passwords like "12345" | Screenshot of registration success |

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

---
