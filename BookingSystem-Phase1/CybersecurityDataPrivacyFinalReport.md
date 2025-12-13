# Cybersecurity and Data Privacy – Final Report

## PortSwigger

### SQL injection
- SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
- SQL injection vulnerability allowing login bypass
### Cross-site scripting
- Reflected XSS into HTML context with nothing encoded
- Stored XSS into HTML context with nothing encoded
- Reflected XSS into attribute with angle brackets HTML-encoded
- Stored XSS into anchor href attribute with double quotes HTML-encoded
### Cross-site request forgery (CSRF)
- CSRF vulnerability with no defenses
### Access control vulnerabilities
- Unprotected admin functionality
- Unprotected admin functionality with unpredictable URL
- User role controlled by request parameter
- User role can be modified in user profile
- User ID controlled by request parameter
- User ID controlled by request parameter, with unpredictable user IDs
- User ID controlled by request parameter with data leakage in redirect
- User ID controlled by request parameter with password disclosure
- Insecure direct object references
### Authentication
- Username enumeration via different responses
- 2FA simple bypass
- Password reset broken logic

<img width="1155" height="933" alt="Portswigger" src="https://github.com/user-attachments/assets/6c100210-7b8b-4dae-8810-e9bd73a3787b" />

## The Booking System Project

### Phase 1
In Phase 1, the purpose was to evaluate The Booking System -web applications user rgistration functionality. The testing was conducted using gray-box approach in a local Docker-based enviroment. Testing was done with manual tests and with automated OWASP ZAP scan. These were used to evaluate input validation, error handling, role assignment, password handling and backend behaviour during account creation. Database and container logs were also used to support the analysis.

As part of Phase 1, the testing was repeated on an updated version of the application (Part 2). Previously identified findings were re-tested to verify whether fixes had been applied. A second OWASP ZAP scan was performed, and the results were documented in a separate report.

#### What worked / didin't work
MAnual testing and ZAP scan provided a good overview of critical weaknesses early in the project.

#### What took the most time
Setting up the setup wit docker/debian, conducting manual tests and analyzing server errors, database behaviour.

#### What I learned
I learned how complex even basic functionality like registration can be in sense of cybersecurity. Also lots of ways to tests vulnerabilities and to evaluete the risk of these vulnerabilities.


### Phase 2
In Phase 2, the Booking System application was tested again using an updated version of the system. The testing followed the same methodology as in Phase 1, including both manual testing and automated OWASP ZAP scanning.

In addition to general security testing, Phase 2 focused on password security an d cracking methods. Multiple password hashes were cracked following course material which included hints and guides for this. The cracking process, tools used, and results were documented.

#### What worked / didin't work
Repeating the tests made it easier to identify changes between application versions and to verify whether previous issues had been mitigated. Password cracking exercises clearly demonstrated the weaknesses of poor password handling. Some automated findings still required manual verification to determine their actual impact.

#### What took the most time
Password cracking and documenting the process step by step, including validating results and capturing evidence.

#### What I learned
I learned how attackers can exploit weak password practices and why proper hashing, salting, and password policies are critical. I also gained a better understanding of the difference between dictionary-based and non-dictionary attacks, and how access to a database significantly increases an attacker’s capabilities.

### Phase 3
In Phase 3, the focus was on authorization testing of the Booking System -web application. The goal was to verify that access control is correctly enforced for all user roles (Guest, Reserver, and Administrator). There were given specific specifications and functionality was tested keeping these in mind. Testing was performed using browser baed testing, API request manipulation, OWASP ZAP scan and endpoint discovery with Gobuster and Wfuzz. All accessible pages, functions, and API endpoints were tested for each role.

#### What worked / didin't work
Role-based testing clearly exposed authorization weaknesses that were not visible in earlier phases. However, the lack of proper HTTP error codes (missing 404 responses) limited the effectiveness of fuzzing tools and required more manual verification.

#### What took the most time
Systematic testing of all roles across UI and API endpoints, as well as verifying backend authorization independently of frontend behavior.

#### What I learned
I lerned how critical a proper backend authorization checks are and how easily easily severe vulnerabilities can occur if access controlis not enforced properly (such as IDOR).

### Phase 4
Phase 4 focused on GDPR compliance in the Booking System application. The goal was to evaluate how personal data is collected, processed, stored, dossclosed and how these were documented and shoen to the user. GDPR checklist was completede evaluating these things and proper Privacy Policy ,Terms of Servuce and Cookie Policy documetns were made for the application.

#### What worked / didin't work
Structured GDPR checklist helped to systematically evaluate Booking System application from GDPR perspective.

#### What took the most time
Evaluating GDPR recommendations trhough UI and backend logs/SQL.

#### What I learned
I learned that GDPR  is not only about having a correct policies, but also about how the system is technically designed. Data protection is better to be build in system from the start rather than beginning to implement it afterwards.

### Overall Reflection
During this course, I learned how real world web application security testing is performed in an iterative and systematic way. I gained practical experience with manual testing, automated tools such as OWASP ZAP, and authorization testing across different user roles. The project demonstrated how critical backend validation and access control are, especially when preventing issues like IDOR and privilege escalation. GDDPR phase was also educational about how closely connected security and privacy are connected. Also POrtswigger enviroment was/is really good place to get knowledge considering cybersecurity field and I will be continuing to pass those labs even after the course. Overall, the course significantly improved my understanding of both technical and regulatory aspects of cybersecurity.

## Logbook
🔗 **Logbook:**  
[Logbook (README.md)](https://github.com/MarkkuNiemi/CybersecurityAndDataPrivacy-course-2025#logbook)

### Total hours
71,5h

### Hours per topic
- Cisco course: 8,5h
- Portswigger: roughly 16h
- Phase 1: 18,5h
- Phase 2: 6,5h
- Phase 3: 11,5h
- Phase 4: 5h
- Other: 5,5

