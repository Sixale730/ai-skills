---
name: security-auditor
description: Continuous security vulnerability scanning for OWASP Top 10, common vulnerabilities, and insecure patterns.
allowed-tools: Read, Grep, Bash
---

# Security Auditor Skill

Automatic security vulnerability detection. Scans for SQL injection, XSS, secrets exposure, auth issues, insecure deserialization, CSRF, CORS misconfiguration.

Severity levels: CRITICAL (exploitable), HIGH (weaknesses), MEDIUM (potential), LOW (best practices).

Alert format: severity, location, fix, OWASP/CWE reference.
