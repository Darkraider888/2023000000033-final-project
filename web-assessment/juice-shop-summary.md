# OWASP Juice Shop Assessment Summary

## Completed Tasks
- Completed all 8 tasks in TryHackMe “OWASP Juice Shop” room (100%).
- Focused on three critical web vulnerabilities.

## Vulnerability 1: SQL Injection – Login Bypass

**Description**  
The login form was vulnerable to SQL injection. Entering `' OR 1=1--` as email and any password allowed authentication as the first user (administrator).

**Security Impact**  
Attacker gains admin privileges, can view/modify all user data, place fake orders, and escalate to server compromise.

**Remediation**  
- Use parameterized queries / prepared statements.
- Apply input validation (allowlist characters).
- Deploy a WAF with SQL injection rules.

---

## Vulnerability 2: Stored Cross-Site Scripting (XSS)

**Description**  
The product review field accepted unsanitized input. Injecting `<script>alert('XSS')</script>` stored the payload, which executed when any user viewed the product page.

**Security Impact**  
Attacker can steal session cookies, deface the website, or redirect victims to malicious sites.

**Remediation**  
- Encode output contextually (HTML entity encoding).
- Implement Content Security Policy (CSP) to block inline scripts.
- Sanitize user input with libraries like DOMPurify.

---

## Vulnerability 3: Weak Authentication – Password Reset Poisoning

**Description**  
The password reset functionality derived the reset link from the `Host` header without validation. An attacker can forge the header to point to their own server, intercepting the reset token.

**Security Impact**  
Account takeover – attacker can reset any user’s password and gain full access.

**Remediation**  
- Ignore `Host` header; use a canonical URL defined server-side.
- Send reset tokens out-of-band (e.g., email with a unique, short-lived link).
- Implement rate limiting and CAPTCHA on password reset.
