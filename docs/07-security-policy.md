# Security Policy - Service Manager

Name: Security Policy - `Service Manager`
Version: 1.0.0
Status: Active
Classification: Internal
Last updated: 2026-11-05
Owner: Roman Zaitsev
Related documents: [06-security.md](06-security.md), [07-security-policy.md](07-security-policy.md), [09-threat-model.md](09-threat-model.md)

## Purpose

This policy sets mandatory rules for secure development and maintenance of Service Manager, a web application for small repair workshops. It must ensure confidentiality of client data, credentials and secrets; integrity of orders, inventory and status history; availability of the application to staff; and traceability of critical actions. It covers all life-cycle stages. Threats are described in 09-threat-model.md; concrete software requirements SEC-* are in 06-security.md.

## Scope

The policy applies to the whole GitHub repository `src/`, `tests/`, `docs/`, the .NET MVC application, client-side code, the database, configuration, scripts, NuGet dependencies, and developer workstations in the part that concerns repository access and secrets. Out of scope: the server operating system, physical security, the user's device and browser, and internals of third-party libraries. It is mandatory for the developer, reviewers and any AI tool that changes project files.

## Roles and Responsibilities

| Role | Holder | Responsibility |
| --- | --- | --- |
| Project owner | Roman Zaitsev | Approves the policy and exceptions; accepts residual risk |
| Developer | Roman Zaitsev | Implements requirements, manages secrets, fixes vulnerabilities |
| Reviewer | Roman Zaitsev (self-review in a Pull Request) | Reviews every change before merging; uses a checklist for authentication, authorization and secrets |
| Project supervisor | Course instructor | Checks compliance with course requirements |
| Manager / Technician | Workshop staff | Use the application within their role; keep passwords secret |

The project has one developer, so roles are combined. An AI tool is only a technical assistant: it does not approve changes, weaken requirements or access secrets.

## Security Principles

1. **Least privilege.** A Technician has access only to assigned orders.
2. **Deny by default.** Operations not explicitly allowed are forbidden; new endpoints require authentication.
3. **Secure by default.** HTTPS, anti-forgery protection and role checks work without extra settings.
4. **Defense in depth.** Validation, server-side role checks, parameterized queries and output encoding are all applied.
5. **The client is not trusted.** Validation and authorization are always repeated on the server.
6. **Trust boundaries.** Data crossing a boundary from 09-threat-model.md is validated or protected.
7. **Fail securely.** On error the operation is denied and a generic message is shown.
8. **No secrets in source code.** Passwords, keys and connection strings with passwords never enter the repository.

## Secure Development Environment

- **Repository.** Code is stored on GitHub; only the owner has access. Authentication uses SSH keys; private keys stay on the developer's machine. Two-factor authentication is enabled on the GitHub account.
- **Branches.** Direct commits to `main` are forbidden; branch protection requires a Pull Request. Work is done in `feature/`, `fix/` or `docs/` branches. Commit format is defined in 05-dev-policy.md.
- **Secrets.** Secrets are kept in .NET user-secrets (development) or environment variables (server). `.gitignore` contains `.env`, `appsettings.Development.json`, `*.pfx`, `*.db`, `*.sqlite`, `*.log`. `appsettings.json` is committed and contains no secrets. A secret committed by mistake is treated as compromised: it is revoked and replaced first, then removed from the repository.
- **Dependencies.** Packages come only from the official NuGet registry. Before adding one, its origin, license, maintenance status and known vulnerabilities are checked. Unused packages are removed.
- **AI tools.** Their output is untrusted and goes through the same review and checks as manual code. Secrets and real client data are never given to them.

## Software Protection

- Binaries `bin/`, `obj/` are not committed; builds are made with `dotnet build` / `dotnet publish`.
- The production database is not publicly accessible and is not stored in the repository.
- Database backups are made regularly and stored separately from the server; restore is tested before the first release and after schema changes.
- Secrets, personal data and database dumps must not appear in logs, issues, documentation screenshots or build output.
- Only the owner has access to server configuration and the database.

## Secure Implementation

Requirement IDs refer to 06-security.md.

- **Input and output.** All input is untrusted and validated on the server NFR-1. User data is encoded on output, including printable documents SEC-14. Database access uses an ORM or parameterized queries only SEC-3.
- **Authentication.** Passwords are stored only as salted hashes via ASP.NET Core Identity or an equivalent library SEC-1. Failed logins are limited SEC-8. Session cookies are `HttpOnly`, `Secure`, `SameSite`, and sessions expire after inactivity SEC-13.
- **Authorization.** Every protected action checks the role on the server SEC-2. Every request with an order ID checks ownership SEC-9. Status changes follow the defined sequence SEC-15.
- **Business integrity.** Stock deduction and cost calculation run in a transaction; the part price comes from the database, not from the request SEC-10.
- **Transport and cryptography.** The application is served only over HTTPS SEC-5. Own cryptographic algorithms are forbidden.
- **Errors and logging.** Users see generic errors without stack traces or queries SEC-7. Status changes, stock deductions and logins are logged with user and time SEC-6. Logs contain no passwords, tokens, connection strings or full phone numbers SEC-12.
- **Forbidden.** Disabling anti-forgery protection, certificate validation or authorization attributes; hard-coded credentials; default accounts and debug endpoints in production.

## Security Verification

| Check | When | Method |
| --- | --- | --- |
| Automated tests | Every change | `dotnet test` |
| Compiler warnings | Every change | Warnings treated as errors where possible |
| Self-review of the diff | Every change | Pull Request, tab "Files changed"; look for secrets and debug code |
| Manual review with checklist | Changes to authentication, authorization, roles, secrets, stock logic | Server-side role check, ownership check, parameterized queries, output encoding |
| Dependency check | When dependencies change and before a release | `dotnet list package --vulnerable --include-transitive` |
| Negative tests | Authorization and validation | A Technician cannot open a foreign order; negative quantity, insufficient stock and invalid status transitions are rejected |

**Release gate.** A release is blocked if tests fail, a known critical or high vulnerability has no fix or accepted exception, a secret is found in the repository, or a "Must" requirement from 06-security.md is not satisfied.

## Vulnerability Management

1. Each confirmed vulnerability is recorded as a GitHub Issue with the label `security`: component, impact, steps to reproduce, priority. Details are not published while the fix is pending.
2. The owner sets the priority: Critical, High, Medium or Low.
3. The fix is made in a `fix/<name>` branch through a Pull Request. Target time: Critical and High within 7 days or before the next release; Medium within 30 days.
4. Every fix has a test that fails before the fix and passes after it.
5. If the cause is a gap in architecture or rules, 09-threat-model.md, 06-security.md and this policy are updated.
6. A leaked secret is revoked and replaced immediately.

## Privacy Policy

Rules for personal data are defined in the separate document 08-privacy-policy.md, because it may later be published to users while this policy stays internal.

## Exceptions

A deviation is allowed only with a written justification, GitHub Issue with the label `policy-exception`, a risk description, compensating measures and approval by the project owner. Every exception has an expiration date and is reviewed afterwards. Exceptions to the rules on secrets in the repository and on server-side role checks are not allowed.

## Related Documents

[01-project-description.md](01-project-description.md), [02-requirements-spec.md](02-requirements-spec.md), [03-architecture.md](03-architecture.md), [04-business-logic.md](04-business-logic.md), [05-dev-policy.md](05-dev-policy.md), [06-security.md](06-security.md), [08-privacy-policy.md](08-privacy-policy.md), [09-threat-model.md](09-threat-model.md). External guidance: NIST SP 800-218 (SSDF), OWASP ASVS.

## Final Provisions

The policy takes effect after approval by the project owner on the date in the header. It is reviewed at least once per development phase and after significant changes of architecture, stack, processed data or threat model, or after a security incident. Every change is a separate `[DOCS]` commit with a version increase. If the policy contradicts another document, the stricter requirement applies until the documents are aligned.