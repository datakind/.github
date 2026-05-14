# .github

This repository contains organization-wide community health files for [DataKind](https://github.com/datakind). These files automatically apply to all repositories in the DataKind GitHub organization that don't have their own local versions.

## What's in here

| File | Purpose |
|---|---|
| `CONTRIBUTING.md` | Contribution guidelines, branching strategy, PR process, testing requirements, and approval workflow |
| `.github/PULL_REQUEST_TEMPLATE.md` | Standard pull request template with SOC 2 change management checklist |
| `CODE_OF_CONDUCT.md` | Organization-wide code of conduct |
| `SECURITY.md` | Security vulnerability reporting policy |


## How it works

GitHub automatically uses these files as defaults for any repo in the organization that doesn't have its own copy. For example, when someone opens a pull request on any DataKind repo, they'll see the standard PR template — unless that repo has its own template.

**A repo can override any of these files** by adding its own version locally. The local copy always takes precedence.

## Who can edit

Changes to this repository affect all DataKind repos that inherit from it. Write access is restricted to authorized personnel. If you'd like to propose a change, open a pull request.