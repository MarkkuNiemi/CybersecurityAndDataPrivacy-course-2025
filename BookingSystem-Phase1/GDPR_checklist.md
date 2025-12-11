# GDPR Compliance Checklist – Web-based Booking System

| **Result** | **Personal data mapping and minimization** |
| :----: | :--- |
| &nbsp;⚠️&nbsp; | Collected information is presented for the user, but there isn't any documetnation for what use these informations are collected. |
| &nbsp;✅ OR ⚠️&nbsp; | The personal data that is collected is minimal for the usage of the web application. However if this needs to be documented and presented to user clearly, then it results in "*Attention*" |
| &nbsp;⚠️&nbsp; | Birthdate field exists and web application ensures that user is over 15 years old. Nevertheless it does not explain the need of this data collection for user nor the need to be over 15 years old. |

---

| **Result** | **User registration and management** |
| :----: | :--- |
| &nbsp;❌&nbsp; | The form only contains a checkboc for Terms of Service, but there is no information about the terms in link provided. Privacy Policy is missing and infomration about how personal data is processed is also missing. |
| &nbsp;❌&nbsp; | User can only view own personal data, but cannot delete or edit it. |
| &nbsp;❌&nbsp; | Administrator cannot delete reserver user. There is also no information what happens to the personal data if user could be deleted. |
| &nbsp;✅&nbsp; | In registration birthdate is forced to be over 15 years. |

---

| **Result** | **Booking visibility** |
| :----: | :--- |
| &nbsp;✅&nbsp; | Non-logged  users can see reservations without any personal data. |
| &nbsp;⚠️&nbsp; | In application, personal data is not visible for anyone that is not authorized for that data. Explicits are not documented or this way guaranteed outside the application.  |

--- 

| **Result** | **Access control and authorization** |
| :----: | :--- |
| &nbsp;❌&nbsp; | Resources can be created by any user and reservations can be modified by any user, including other users than the reserver of the reservation. |
| &nbsp;✅&nbsp; | Role-based access control is implemented. |
| &nbsp;⚠️&nbsp; | Administrator privileges are technically very limited, there is no user control panel and for this no user data is visible for admin. There is no documetnation describing data acces rules or restrictions.  |

---

| **Result** | **Privacy by Design Principles** |
| :----: | :--- |
| &nbsp;⚠️&nbsp; | Minimal fields are collected, but processing transparency is lacking. |
| &nbsp;❌&nbsp; | Ther is no documentation what data the system is collecting, how long it is retained or is personal data excluded from logs. Because GDPR requires transparency and data minimization also for log data, this requirement is not fulfilled. |
| &nbsp;⚠️&nbsp; | The forms collect only minimal required data and and it is not visible in UI. However there is no documentation of Privacy by Design practises. Also the application does not provide information about secure data handling or protection mechanisms |

---

| **Result** | **Data security** |
| :----: | :--- |
| &nbsp;⚠️&nbsp; | The application does not provide documentation about CSRF, XSS or SQL injection protections. Without security documentation, GDPR safeguard requirements cannot be confirmed. Technically from ZAP report we can see there is no vulnerability. |
| &nbsp;⚠️&nbsp; | Passwords are securely stored using the BCrypt hashing as seen from the database. However, the application does not document its password protection practises in the Privacy POlicy or Terms of Service.  |
| &nbsp;❌&nbsp; | The application provides no information about data backup or recovery processes. GDPR requires documented policies describing how personal data is backed up, how long it is retained, where it is stored (EU/EEA), and how restoration procedures protect individuals’ data. |
| &nbsp;❌&nbsp; | The application does not provide information about where personal data is stored. |

---

| **Result** | **Data anonymization and pseudonymization** |
| :----: | :--- |
| &nbsp;❌&nbsp; | No anonymization is implemented on personal data. |
| &nbsp;❌&nbsp; | No pseudonymization techniques used to protect data. All personal data remains directly identifiable. |

---

| **Result** | **Data subject rights** |
| :----: | :--- |
| &nbsp;❌&nbsp; | There is no feature in application for user to download own personal data. |
| &nbsp;❌&nbsp; | There is no possibility to request deletion of users personal data. |
| &nbsp;❌&nbsp; | The application does not collect GDPR-compliant consent for data processing, and therefore users cannot withdraw it. |

---

| **Result** | **Documentation and communication** |
| :----: | :--- |
| &nbsp;❌&nbsp; | Privacy policy page exists, but is entirely blank. |
| &nbsp;❌&nbsp; | The system provides no documentation for administrators or developers regarding data protection practises or process activities. |
| &nbsp;❌&nbsp; | There is no documented process for responding to data breaches. |

---

**Symbols used:**  
✅ Pass (a note can be added)  
❌ Fail (a note can be added)  
⚠️ Attention (a note can be added)
