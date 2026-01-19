## SQL Injection – UNION Attack Retrieving Multiple Values in a Single Column

Platform: PortSwigger Web Security Academy  
Lab: SQL injection UNION attack, retrieving multiple values in a single column

---

## Vulnerability Type
UNION-based SQL Injection

---

## Description
The application is vulnerable to SQL injection, allowing attackers to use the UNION operator to manipulate the backend SQL query. In this scenario, only one column is reflected in the HTTP response, which requires concatenating multiple values into a single visible column.

---

## Payloads Used

```sql
'+UNION+SELECT+NULL,'abc'--
```

```sql
'+UNION+SELECT+NULL,username||'~'||password+FROM+users--
```

---

## Technical Impact
By identifying the only text-reflecting column and concatenating multiple database fields into a single output value, it was possible to extract usernames and passwords from the users table despite output limitations imposed by the application.

---

## Risk
An attacker could exploit this vulnerability to obtain valid user credentials, leading to account compromise, unauthorized access, and potential data breaches.

---

## Mitigation
Use prepared statements and parameterized queries to prevent SQL injection. Avoid building dynamic SQL queries with user input and apply strict input validation.
