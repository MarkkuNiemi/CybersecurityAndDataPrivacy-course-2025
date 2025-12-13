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

#### What worked / didin't work


#### What took the most time


#### What I learned


### Phase 3
### Phase 4

### Overall Reflection

## Logbook

## Feedback
