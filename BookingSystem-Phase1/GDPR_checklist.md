# GDPR Compliance Checklist – Web-based Booking System

| **Result** | **Personal data mapping and minimization** |
| :----: | :--- |
| &nbsp;⚠️&nbsp; | Collected information is presented for the user, but there isn't any documetnation for what use these informations are collected. |
| &nbsp;✅/⚠️&nbsp; | The personal data that is collected is minimal for the usage of the web application. However if this needs to be documented and presented to user clearly, then it results in "*Attention*" |
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
| &nbsp;✅/❌/⚠️&nbsp; | Are administrator privileges limited to ensure GDPR compliance (e.g., administrators<br> cannot use data for unauthorized purposes)? |

---

| **Result** | **Privacy by Design Principles** |
| :----: | :--- |
| &nbsp;✅/❌/⚠️&nbsp; | Has Privacy by Default been implemented (e.g., collecting the minimum data by default)? |
| &nbsp;✅/❌/⚠️&nbsp; | Are logs implemented without unnecessarily storing personal data? |
| &nbsp;✅/❌/⚠️&nbsp; | Are forms and system components designed with data protection in mind<br> (e.g., secured login, minimal fields)? |

---

| **Result** | **Data security** |
| :----: | :--- |
| &nbsp;✅/❌/⚠️&nbsp; | Are CSRF, XSS, and SQL injection protections implemented? |
| &nbsp;✅/❌/⚠️&nbsp; | Are passwords securely hashed using a strong algorithm (e.g., bcrypt, Argon2)? |
| &nbsp;✅/❌/⚠️&nbsp; | Are data backup and recovery processes GDPR-compliant? |
| &nbsp;✅/❌/⚠️&nbsp; | Is personal data stored in data centers located within the EU? |

---

| **Result** | **Data anonymization and pseudonymization** |
| :----: | :--- |
| &nbsp;✅/❌/⚠️&nbsp; | Is personal data anonymized where possible? |
| &nbsp;✅/❌/⚠️&nbsp; | Are pseudonymization techniques used to protect data while maintaining its utility? |

---

| **Result** | **Data subject rights** |
| :----: | :--- |
| &nbsp;✅/❌/⚠️&nbsp; | Can users download or request all personal data related to them (data access request)? |
| &nbsp;✅/❌/⚠️&nbsp; | Is there an interface or process for users to request the deletion of their personal data? |
| &nbsp;✅/❌/⚠️&nbsp; | Can users withdraw their consent for data processing? |

---

| **Result** | **Documentation and communication** |
| :----: | :--- |
| &nbsp;✅/❌/⚠️&nbsp; | Is there a privacy policy available to users during registration and easily accessible? |
| &nbsp;✅/❌/⚠️&nbsp; | Are administrators and developers provided with documented data protection practices <br>and processing activities? |
| &nbsp;✅/❌/⚠️&nbsp; | Is there a documented data breach response process (e.g., how to notify authorities <br>and users of a breach)? |

---

**Symbols used:**  
✅ Pass (a note can be added)  
❌ Fail (a note can be added)  
⚠️ Attention (a note can be added)
