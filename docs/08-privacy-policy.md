# Privacy Policy - Service Manager

Name: Security Policy - `Service Manager`
Version: 1.0.0
Status: Active
Classification: Internal
Last updated: 2026-11-05
Owner: Roman Zaitsev
Related documents: [06-security.md](06-security.md), [07-security-policy.md](07-security-policy.md), [09-threat-model.md](09-threat-model.md)

## Purpose and scope

This document describes what data Service Manager processes, why, where it is stored, who can access it and how long it is kept. It applies to the application, its database, logs and backups. It is a separate document because it may later be shown to users, while [07-security-policy.md](07-security-policy.md) stays internal. The workshop that uses the system is responsible for observing the applicable personal data legislation (including the Law of Ukraine "On Personal Data Protection").

## Categories of data

| Category | Data |
| --- | --- |
| Client data | Full name, phone number |
| Order data | Device model, fault description, status history, comments, used parts, cost |
| Account data | Username, password hash, role (Manager or Technician) |
| Audit and technical data | User, time and type of status changes, stock deductions, logins; error logs |

**Not collected:** email, home address, date of birth, identification numbers, payment data, geolocation, special categories of data. Clients have no accounts in the system.

## Sources and purposes

- Client and order data is entered by a Manager when a device is accepted. It is used only to carry out the repair, contact the client and issue the Acceptance Receipt and Certificate of Completion.
- Account data is used only for authentication and access control.
- Audit data ensures accountability of critical actions (SEC-6).
- Data is not used for marketing or profiling.

## Storage, access and sharing

- Data is stored in the application database on the workshop server. The database and backups are not publicly accessible.
- Manager has access to all clients and orders. Technician has access only to assigned orders. The project owner has technical access for maintenance only. Access is checked on the server (SEC-2, SEC-9).
- Data is not sold or transferred to third parties, because the system has no external integrations. It is disclosed only if required by law. Before any integration is added, this document and [09-threat-model.md](09-threat-model.md) must be updated.

## Retention and deletion

| Data | Retention | After the period |
| --- | --- | --- |
| Client and order data | 3 years after the client's last order | Deleted or anonymized |
| Account data | While the person uses the system | Disabled, then deleted; audit records keep only an internal user ID |
| Audit data | 3 years | Deleted |
| Application logs | 90 days | Deleted |
| Backups | 30 days | Overwritten |

A client may ask the workshop to correct or delete their data. Data that must be kept by law or for a warranty dispute is kept until the required period ends.

## Logging and protection

The following must not be written to logs, error messages, issues or commits (SEC-12): passwords and hashes, session cookies, tokens, keys and connection strings, full phone numbers and names (internal IDs are used instead).

Protection measures: HTTPS for all traffic (SEC-5), salted password hashes (SEC-1), parameterized queries (SEC-3), secrets outside the repository (SEC-11), backups stored separately from the server and encrypted where possible. Real client data is not used in development, tests, documentation or AI tools; test data is synthetic.

## Data minimization and changes

Only data needed for repairs is collected. Every new field with personal data needs a documented purpose and must be added to this document before implementation. The policy is reviewed together with [07-security-policy.md](07-security-policy.md). Changes are committed with the prefix `[DOCS]` and a version increase.

Contact: the project owner, Roman Zaitsev, via the project repository.
