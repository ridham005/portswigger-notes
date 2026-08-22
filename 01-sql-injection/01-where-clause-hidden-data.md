Vulnerability: SQL Injection in WHERE clause parameter.

Target: /filter?category=

Payload: '+OR+1=1--

Remediation: Implement parameterized prepared statements in the SQL query backend.