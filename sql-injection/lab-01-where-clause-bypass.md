# SQL Injection – WHERE Clause Bypass

**Platform:** PortSwigger Web Security Academy  
**Lab:** SQL injection vulnerability in WHERE clause  

---

## Vulnerability Type
Boolean-based SQL Injection

---

## Description
The application directly concatenates user input from the `category` parameter into a SQL query without proper sanitization.

---

## Payload Used

' OR 1=1--


---

## Technical Impact
The injected condition always evaluates to true, bypassing the business logic that restricts access to unreleased products.

---

## Risk
An attacker could manipulate SQL queries to access sensitive information from the database.

---

## Mitigation
Use prepared statements (parameterized queries) to prevent user input from being interpreted as SQL code.

## Mitigation
Use prepared statements (parameterized queries) to prevent user input from being interpreted as SQL code.
