# .github

Org-wide defaults for [DataKind](https://github.com/datakind): community health files (auto-inherited) and reusable workflows (opt-in per repo).

## Community health files

| File | Purpose |
|---|---|
| `CONTRIBUTING.md` | Branching, PR process, testing, approvals |
| `.github/PULL_REQUEST_TEMPLATE.md` | PR template with SOC 2 checklist |
| `CODE_OF_CONDUCT.md` | Code of conduct |
| `SECURITY.md` | Vulnerability reporting |

Repos override any of these by adding a local copy.

## Reusable workflows

Live under `.github/workflows/`. Not inherited — add a caller in each repo:

```yaml
jobs:
  example:
    uses: datakind/.github/.github/workflows/<name>.yml@main
```

| Workflow | Purpose | Caller trigger |
|---|---|---|
| `enforce-pr-targets` | PRs to `main` only from `release/*` or `hotfix/*` | `pull_request` → `develop`, `main` |
| `pr-title` | Conventional Commits PR titles | `pull_request` (opened, edited, synchronize) |
| `pre-release` | `CHANGELOG.md` required on PRs to `main` | `pull_request` → `main` |
| `dependency-review` | Dependency Review on PRs | `pull_request` |

### Caller examples

```yaml
# enforce-pr-targets
jobs:
  enforce:
    uses: datakind/.github/.github/workflows/enforce-pr-targets.yml@main

# pr-title
jobs:
  validate:
    permissions:
      pull-requests: read
    uses: datakind/.github/.github/workflows/pr-title.yml@main

# pre-release
jobs:
  check:
    permissions:
      pull-requests: read
    uses: datakind/.github/.github/workflows/pre-release.yml@main

# dependency-review
permissions:
  contents: read
jobs:
  review:
    uses: datakind/.github/.github/workflows/security.yml@main
```

`pr-title` accepts optional `types` input (multiline). Defaults include `model`.

## Who can edit

Changes here affect all org repos that inherit from it. Open a PR to propose changes.
