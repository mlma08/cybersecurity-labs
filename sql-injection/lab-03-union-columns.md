# SQL Injection – UNION Attack Column Enumeration

**Platform:** PortSwigger Web Security Academy  
**Lab:** SQL injection UNION attack, determining the number of columns  

---

## Vulnerability Type
UNION-based SQL Injection

---

## Description
The application is vulnerable to SQL injection, allowing attackers to append arbitrary SQL queries using the UNION operator. This vulnerability enables an attacker to infer the internal structure of the backend SQL query.

---

## Payload Used

UNION SELECT null,null,null--


---

## Technical Impact
By injecting a UNION SELECT statement with three NULL values, it was possible to determine that the original SQL query contains exactly three columns. Matching the number of columns is a prerequisite for further UNION-based SQL injection attacks.

---

## Risk
An attacker could leverage this vulnerability to construct more advanced UNION queries to extract sensitive data from the database, including user credentials and internal system information.

---

## Mitigation
Implement parameterized queries and prepared statements to prevent user input from being interpreted as SQL code. Additionally, apply strict input validation and use least-privilege database accounts.
