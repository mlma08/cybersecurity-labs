# SQL Injection – UNION Attack Retrieving Data from Other Tables

**Platform:** PortSwigger Web Security Academy  
**Lab:** SQL injection UNION attack, retrieving data from other tables  

---

## Vulnerability Type
UNION-based SQL Injection

---

## Description
The application is vulnerable to SQL injection, allowing attackers to append arbitrary SQL queries using the UNION operator. This vulnerability enables extraction of sensitive information from other database tables.

---

## Payload Used

```sql
UNION SELECT username, password, NULL FROM users--
```

## Technical Impact
By leveraging the UNION operator, it was possible to retrieve sensitive data from the users table, including valid usernames and passwords. This demonstrates that an attacker can fully compromise the confidentiality of the database.

---

## Risk
An attacker could extract user credentials, leading to account takeover, large-scale data breaches, and full system compromise.

---

## Mitigation
Use prepared statements and parameterized queries to prevent SQL injection. Enforce strict input validation and apply the principle of least privilege to database accounts.
