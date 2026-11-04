# 05. Development Policy

## Version control
- The project is stored in Git and hosted on GitHub.
- Private keys and passwords are never committed.

## Branches
- `main` - the stable version of the project.
- New work is done in separate branches `feature/...`, `fix/...` and merged into `main` when it is ready.

## Commit messages
Format: `[PREFIX] Short description`

- `[INIT]` - project initialisation
- `[FEAT]` - new feature
- `[FIX]` - bug fix
- `[DOCS]` - documentation

## Rules
- Documentation is updated before or together with code changes.
- All user input is validated.
- A change is finished when it works, is tested and is documented.