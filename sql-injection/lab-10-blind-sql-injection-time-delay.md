## Blind SQL Injection with Time Delays

Platform: PortSwigger Web Security Academy  
Lab: Blind SQL injection with time delays

---

## Vulnerability Type
Blind SQL Injection (Time-Based)

---

## Description
The application is vulnerable to blind SQL injection via the TrackingId cookie. The vulnerability does not return database data, error messages, or visible indicators in the response. Instead, successful injection can be confirmed by observing a deliberate delay in the application's response time.

This behavior indicates that user-controlled input is executed directly within a backend SQL query.

---

## Payloads Used

### Time-based injection confirmation

```sql
TrackingId=x'||pg_sleep(10)--
```

---

## Observed Behavior
After sending the injected payload, the application response was delayed by approximately 10 seconds. The delay was consistent and reproducible, confirming that the injected SQL function was executed by the database.

---

## Technical Impact
By leveraging time-based blind SQL injection techniques, it is possible to confirm vulnerable injection points even when no output or error messages are returned. This technique can be extended using conditional time delays to infer database structure and extract sensitive information.

---

## Risk
An attacker could exploit this vulnerability to silently enumerate the database and extract confidential data without triggering visible errors or alerts, making detection significantly more difficult.

---

## Mitigation
Use parameterized queries and prepared statements to prevent SQL injection. Avoid dynamically constructing SQL queries with user input and ensure proper backend validation and sanitization.
