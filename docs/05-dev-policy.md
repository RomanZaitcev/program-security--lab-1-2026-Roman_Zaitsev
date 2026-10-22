# 05. Development Policy

## 1. Version control
- Git is used, the remote repository is hosted on GitHub.
- Authentication to GitHub uses SSH keys. Private keys are never committed or shared.

## 2. Branches
| Branch | Purpose |
|---|---|
| `main` | Stable, reviewed state of the project |
| `feature/<name>` | New functionality |
| `fix/<name>` | Bug fixes |
| `docs/<name>` | Documentation changes |

Work is done in a separate branch and merged into `main` only after the checks below.

## 3. Commit messages
Format: `[PREFIX] Short imperative description`

| Prefix | Use |
|---|---|
| `[INIT]` | Project initialisation |
| `[FEAT]` | New feature |
| `[FIX]` | Bug fix |
| `[DOCS]` | Documentation |
| `[TEST]` | Tests |
| `[REFACTOR]` | Code restructuring without behaviour change |
| `[CHORE]` | Build, configuration, dependencies |

One commit = one logical change.

## 4. Specification-driven development
A change in behaviour is first reflected in `docs/` (requirements, business logic), then in code and tests. Documents must be kept consistent with the implementation.

## 5. Code rules
- MVC structure; no business logic in views.
- All user input is validated on the server.
- No secrets (passwords, keys, connection strings with passwords) in the repository.
- Meaningful names; comments explain why, not what.

## 6. Definition of done
- Requirement implemented and linked to its ID.
- Tests written and passing.
- Documentation updated.
- No secrets or debug code committed.

## 7. Dependencies
Dependencies are listed in the project file, kept up to date, and checked for known vulnerabilities before release.
