# SQL Injection – UNION Attack Finding a Text Column

**Platform:** PortSwigger Web Security Academy  
**Lab:** SQL injection UNION attack, finding a column containing text  

---

## Vulnerability Type
UNION-based SQL Injection

---

## Description
The application is vulnerable to SQL injection, allowing attackers to use the UNION operator to inject additional SQL queries. This vulnerability enables identification of which columns can reflect textual data in the HTTP response.

---

## Payload Used

```sql
UNION SELECT NULL,'text',NULL--
```
---

## Technical Impact
By testing different column positions with a string value, it was possible to identify which column accepts and reflects textual data. This column can be used as a data exfiltration channel in subsequent UNION-based SQL injection attacks.

---

## Risk
An attacker could exploit this vulnerability to extract sensitive information such as usernames, email addresses, and password hashes from the database.

---

## Mitigation
Use prepared statements and parameterized queries to prevent SQL injection. Additionally, apply proper input validation and output encoding.
