# SQL Injection – Login Bypass

**Platform:** PortSwigger Web Security Academy  
**Lab:** SQL injection vulnerability allowing login bypass  

---

## Vulnerability Type
Authentication bypass via SQL Injection

---

## Description
The login functionality directly concatenates user input into a SQL query without proper input sanitization, allowing attackers to manipulate the authentication logic.

---

## Payload Used

**administrator'--**

---

## Technical Impact
The injected SQL comment truncates the password validation logic, allowing authentication as the administrator user without knowing the password.

---

## Risk
An attacker could take over user accounts, including administrative accounts, leading to full system compromise.

---

## Mitigation
Implement prepared statements and parameterized queries to prevent user input from being interpreted as SQL code.
