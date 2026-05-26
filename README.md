# .github

This repository contains organization-wide defaults for [DataKind](https://github.com/datakind): community health files that apply automatically, and reusable workflows that repos opt into.

## What's in here

| File | Purpose |
|---|---|
| `CONTRIBUTING.md` | Contribution guidelines, branching strategy, PR process, testing requirements, and approval workflow |
| `.github/PULL_REQUEST_TEMPLATE.md` | Standard pull request template with SOC 2 change management checklist |
| `CODE_OF_CONDUCT.md` | Organization-wide code of conduct |
| `SECURITY.md` | Security vulnerability reporting policy |
| `.github/workflows/enforce-pr-targets.yml` | Reusable workflow: block PRs into production unless sourced from release or hotfix branches |

## Reusable workflows

Unlike community health files, **workflows are not inherited automatically**. Each repo opts in with a thin caller workflow that references this repository:

```yaml
jobs:
  enforce:
    uses: datakind/.github/.github/workflows/enforce-pr-targets.yml@main
```

### `enforce-pr-targets`

Ensures pull requests into the production branch come only from `release/*` or `hotfix/*` branches.

**Caller trigger** — add to the consuming repo (matches the branch model in `CONTRIBUTING.md`):

```yaml
name: enforce-pr-targets

on:
  pull_request:
    branches:
      - develop
      - main

jobs:
  enforce:
    uses: datakind/.github/.github/workflows/enforce-pr-targets.yml@main
```

No extra permissions or secrets are required.

## How it works

**Community health files** — GitHub uses these as defaults for any org repo that doesn't have its own copy (e.g. the standard PR template on pull requests).

**Reusable workflows** — Not inherited. A repo must add a caller workflow with `uses: datakind/.github/...` to enable them.

**A repo can override any of these files** by adding its own version locally. The local copy always takes precedence.

## Who can edit

Changes to this repository affect all DataKind repos that inherit from it. Write access is restricted to authorized personnel. If you'd like to propose a change, open a pull request.