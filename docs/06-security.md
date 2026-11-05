# 06. Security

## What we protect
- Client personal data (name, phone).
- User accounts and passwords.
- Order and inventory data.
- Source code and SSH keys.

## Security requirements
- Passwords are stored only as salted hashes, never as plain text.
- Access rights are checked on the server for every action, so a Technician cannot see Manager data or other technicians' orders.
- The database is accessed only through parameterized queries it is protection from SQL injection.
- All forms use anti-forgery tokens, and user output is encoded.
- The application works over HTTPS.
- Status changes and stock deductions are logged with the user and time.
- Error messages do not reveal internal details.
- Secrets and private keys are kept out of the repository.

## Secure development
- Changes are reviewed before merging into `main`.
- Dependencies are checked for known vulnerabilities before release.
- Found vulnerabilities are recorded, fixed in a separate branch and verified by a test.

## Security requirements from the threat model

Requirement
SEC 8. The number of failed login attempts shall be limited (temporary lockout or delay) to prevent password guessing and request flooding.
SEC 9. Every request that uses an order ID shall check on the server that the order is assigned to the current Technician, or that the user is a Manager.
SEC 10. Stock deduction and cost calculation shall run in a database transaction; the part price and quantity limits shall be taken from the database on the server, not from the request.
SEC 11. Secrets (database password, keys, certificates) shall be stored outside the repository, in user-secrets or environment variables. `appsettings.json` shall not contain secrets.
SEC 12. Logs shall not contain passwords, session tokens, connection strings or full client phone numbers.
SEC 13. Session cookies shall be marked HttpOnly, Secure and SameSite, and sessions shall expire after a period of inactivity.
SEC 14. All user-supplied data (comments, device description, client name) shall be encoded on output, including printable documents.
SEC 15. Order status transitions shall be validated on the server according to the defined sequence (BR-5).
SEC 16. The database shall not be publicly accessible; the application shall use an account with the minimum necessary permissions.
SEC 17. Regular database backups shall be made and stored separately from the server.