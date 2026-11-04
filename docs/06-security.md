# 06. Security

Based on the general practices of NIST SP 800-218 (Secure Software Development Framework).

## What we protect
- Client personal data (name, phone).
- User accounts and passwords.
- Order and inventory data.
- Source code and SSH keys.

## Security requirements
- **SEC-1.** Passwords are stored only as salted hashes, never as plain text.
- **SEC-2.** Access rights are checked on the server for every action, so a Technician cannot see Manager data or other technicians' orders.
- **SEC-3.** The database is accessed only through parameterized queries (protection from SQL injection).
- **SEC-4.** All forms use anti-forgery tokens (CSRF), and user output is encoded (XSS).
- **SEC-5.** The application works over HTTPS.
- **SEC-6.** Status changes and stock deductions are logged with the user and time.
- **SEC-7.** Error messages do not reveal internal details.
- **SEC-8.** Secrets and private keys are kept out of the repository.

## Secure development
- Changes are reviewed before merging into `main`.
- Dependencies are checked for known vulnerabilities before release.
- Found vulnerabilities are recorded, fixed in a separate branch and verified by a test.
