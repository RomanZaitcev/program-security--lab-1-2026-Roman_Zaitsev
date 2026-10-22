# 06. Security

Based on the practices of NIST SP 800-218 (SSDF): prepare the organization, protect the software, produce well-secured software, respond to vulnerabilities.

## 1. Assets
- Client personal data (name, phone).
- User accounts and credentials.
- Order and inventory data.
- Source code and keys.

## 2. Threats and measures

| Threat | Measure |
|---|---|
| Unauthorized access | Authentication, role-based access control, session timeout |
| Weak or stolen passwords | Passwords stored only as salted hashes (e.g. ASP.NET Core Identity), password complexity rules |
| Privilege escalation (Technician reads Manager data) | Server-side role checks on every action, not only hidden UI elements |
| SQL injection | Parameterized queries / ORM only |
| Cross-site scripting (XSS) | Output encoding in views, input validation |
| CSRF | Anti-forgery tokens on all forms |
| Data interception | HTTPS for all traffic |
| Leakage of secrets | Secrets kept outside the repository (`.env`, user secrets), `.gitignore` rules |
| Stock manipulation | Transactional stock deduction, audit of changes |

## 3. Security requirements

| ID | Requirement |
|---|---|
| SEC-1 | All passwords shall be stored as salted hashes. |
| SEC-2 | Every protected action shall check the user's role on the server. |
| SEC-3 | All database access shall use parameterized queries. |
| SEC-4 | All forms shall use anti-forgery tokens. |
| SEC-5 | The application shall be served over HTTPS. |
| SEC-6 | Status changes and stock deductions shall be logged with user and time. |
| SEC-7 | Error messages shall not reveal internal details to the user. |

## 4. Secure development practices
- Review of changes before merging into `main`.
- Dependency vulnerability check before release.
- Static analysis / compiler warnings treated as errors where possible.
- Private SSH keys stay on the developer's machine only.

## 5. Vulnerability handling
Found issues are recorded, prioritized by impact, fixed in a `fix/` branch, and verified by a test.
