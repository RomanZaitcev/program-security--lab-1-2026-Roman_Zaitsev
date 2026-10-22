# Service Manager

Web application for automating the operations of small service centers and equipment repair workshops.

**Author:** Roman Zaitsev, group SE-23-1, Khmelnytskyi National University
**Course:** Program Security (Lab 1)
**Status:** documentation stage (project initialised, code not yet implemented)

## Summary

Service Manager replaces paper notebooks and Excel sheets with one application. Managers register devices and clients and print receipts. Technicians see their queue, update repair statuses and log used spare parts. The system tracks inventory and deducts parts automatically.

## Documentation

| Document | Description |
|---|---|
| [01 Project description](docs/01-project-description.md) | Purpose, scope, stakeholders |
| [02 Requirements specification](docs/02-requirements-spec.md) | Functional and non-functional requirements (ISO/IEC/IEEE 29148) |
| [03 Architecture description](docs/03-architecture.md) | Stakeholders, viewpoints, views (ISO/IEC/IEEE 42010) |
| [04 Business logic](docs/04-business-logic.md) | Core scenarios and algorithms |
| [05 Development policy](docs/05-dev-policy.md) | Commits, branches, review, definition of done |
| [06 Security](docs/06-security.md) | Security requirements and practices (NIST SP 800-218) |
| [07 Testing](docs/07-testing.md) | Test strategy and acceptance procedure |

## Repository structure

```
docs/    project documentation
src/     source code (.NET, MVC)
tests/   automated tests
```
