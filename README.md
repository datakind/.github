# .github

Org-wide defaults for [DataKind](https://github.com/datakind): community health files and shared CI workflows.

## Community health files

| File | Purpose |
|---|---|
| `CONTRIBUTING.md` | Branching, PR process, testing, approvals |
| `.github/PULL_REQUEST_TEMPLATE.md` | PR template with SOC 2 checklist |
| `CODE_OF_CONDUCT.md` | Code of conduct |
| `SECURITY.md` | Vulnerability reporting |

Repos override any of these by adding a local copy.

## Reusable workflows

Copy [`.github/workflows/ci.yml.example`](.github/workflows/ci.yml.example) to `.github/workflows/ci.yml` in your repo. Comment out jobs you don't need, add local `lint` / `test` jobs, and set repo secret `ASANA_SECRET` for Asana.

| Workflow | Purpose |
|---|---|
| `pr-title` | Validates PR titles |
| `link-asana-task`    | Requires Asana task URL and links PR via API        |
| `dependency-review` | Flags vulnerable dependency changes |
| `enforce-pr-targets` | PRs to `main` only from `release/*` or `hotfix/*` |
| `pre-release` | Requires `CHANGELOG.md` on PRs to `main` |
| `npm-audit` | `npm audit` (Node repos) |
| `composer-audit` | `composer audit` (PHP repos) |

## Who can edit

Changes here affect all org repos that inherit from it. Open a PR to propose changes.
