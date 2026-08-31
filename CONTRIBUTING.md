# Contributing to DataKind Projects

Hi\! Thanks for your interest in contributing to DataKind, we're really excited to see you\! In this document we'll try to summarize everything that you need to know to do a good job. This resource is primarily for community contributions to public repos. 

DataKind staff and contractors should refer to the [Engineering Playbook](https://datakind.atlassian.net/wiki/x/GgBwL) for greater detail on development practices. All contributions on [compliant product repos](https://datakind.atlassian.net/wiki/x/BYAdM) must follow DataKind's [SOC 2 Compliant Change Management Process](https://datakind.atlassian.net/wiki/x/BAAjM).

## New contributor guide

To get an overview of the project, please read the README and our [Code of Conduct](http://CODE_OF_CONDUCT.md) to keep our community approachable and respectable.

## Getting started

### Change Requests

Every change — whether a bug fix, new feature, infrastructure update, or ML model update — begins as an Asana task. GitFlow `release/*` and `hotfix/*` PRs also use Asana (promote / deploy). Exceptions: automated release-please packaging PRs, branch sync (`sync/*`, `chore/sync-*`), and automated dependency updates (`chore(deps)`).

For some products, changes can be submitted through product feedback forms or Github issues to populate Asana. The Asana task must include:

- **Title:** Clear description of the change  
- **Description:** What is changing, why, and what systems are affected  
- **Risk Level:**  
  - High	  
    - Features: Auth changes, database schema changes, infrastructure changes, new AI/ML models to production  
    - Bugs: Major functionality failure, system down, user or sensitive data breached  
    - Typically 100% of users affected  
  - Medium	  
    - Features: API integrations, model retraining, new functionality  
    - Bugs: Friction or slow down of main product function; or minor product feature blocked with no clear workaround  
    - Typically 25-75% of users affected, but varies	  
  - Low	  
    - Features: UI copy changes, non-sensitive config updates  
    - Bugs: Minor product functions slowed down or friction created; or potentially stale data displayed to users  
    - Bug is repeatable and will affect more than one user  
- **Assignee:** Developer responsible for implementation  
- **Linked GitHub PR:** (added once the PR is opened)

## Development

All code is stored in DataKind's GitHub organization at [github.com/datakind](https://github.com/datakind).

### GitHub Workflow

As many open source projects, we often use [gitflow](https://nvie.com/posts/a-successful-git-branching-model/) to manage our branches on DataKind's open source repos.

Summary of our git branching model:

1. Get all the latest work from the upstream repository (`git checkout main`)  
2. Create a new branch off with a descriptive name (for example: `feature/new-login-page`, `hotfix/fix-auth-crash`). You can do it with (`git checkout -b <branch name>`)  
3. Make your changes and commit them locally using [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) (`git add <changed files>`, `git commit -m "feat: Add some change" <changed files>`). Whenever you commit, the self-tests and code quality checks will kick in; fix anything that gets broken.  
4. Push to your branch on GitHub (with the same name as your local branch: `git push origin <branch name>`). This will output a URL for creating a Pull Request (PR)  
5. Create a pull request by opening the URL in a browser. You can also create PRs in the GitHub interface, choosing your branch to merge into `develop`  
6. Wait for comments and respond as-needed.  
7. Once the PR review is complete, your code will be merged. Thanks\!\!

### Branch Naming Convention

| Branch Type | Naming Pattern | Use |
| :---- | :---- | :---- |
| `feature/short-description` | Feature development and dependency updates | Branch from `develop`, merge back to `develop` |
| `release/X.Y.Z` | Release versions | Branch from `develop`, merge to `main` and `develop` |
| `hotfix/X.Y.Z` | Production or release fixes | Branch from `main`, merge back to `main` and `develop` |

Some branch definitions:

- **main**: always stable and release-ready branch. Deployments to production happen only from this branch.  
- **develop**: default branch, contains latest features and fixes, on which developers should orient.  
- **feature-\***: branches for feature development and dependency updates.  
- **release-\***: branches for release versions.  
- **hotfix-\***: branches for production or release fixes.

### Branch Protection Rules

The following rules are enforced in GitHub for all DataKind repositories for products that are under SOC2 compliance:

- `main` / production branch is protected  
- Pull request reviews are required before merging (minimum 1 approver; 2 for High-risk changes)  
- Status checks must pass (CI/CD tests, linting)  
- Direct pushes to `main` are disabled for all users, including admins  
- Signed commits are recommended (will show as "verified" in GitHub)

### Tips

- Write helpful commit messages  
- Anything in your branch must have no failing tests. You can check by looking at your PR online in GitHub  
- Never use `git add .`: it can add unwanted files;  
- Avoid using `git commit -a` unless you know what you're doing;  
- Check every change with `git diff` before adding them to the index (stage area) and with `git diff --cached` before committing;  
- If you have push access to the main repository, please do not commit directly to `main` or `develop`: your access should be used only to accept pull requests; if you want to make a new feature, you should use the same process as other developers so your code will be reviewed.

## Code Review

### Pull Request Guidelines

All pull requests must use the repository's standard PR template. Refer to our [Pull Requests guide in the Engineering Playbook](https://datakind.atlassian.net/wiki/x/AwAaM). Every PR should include:

**Required:**

- Link to the Asana task(s) (not required for release-please packaging or branch sync)  
- Summary of changes made  
- Confirmation that no secrets or credentials are hardcoded

**Recommended:**

- Testing steps / how to verify  
- Screenshots or evidence of testing

Additional guidelines:

- Feature branches should be started from `develop` and merged back to `develop`.  
- Hotfix branches should be started from `main` and must be merged back to `main` and `develop`. It is also possible to start hotfix branches from a release branch and merge back to `main`, `develop`, and the release branch.  
- Any release branch should start from the `develop` branch. Starting a release branch unblocks new feature development. Merging a release branch to `main` indicates a new version in production.

## Testing

You should write tests for every feature you add or bug you solve in the code. Having automated tests for every line of our code lets us make big changes without worries: There will always be tests to verify if the changes introduced bugs or lack of features. If we don't have tests, every change will come with some fear of possibly breaking something.

For a better design of your code, we recommend using a technique called [test-driven development](https://en.wikipedia.org/wiki/Test-driven_development), where you write your tests before writing the actual code that implements the desired feature.

The required testing depends on the type of change. All tests must pass before a PR can be merged.

| Change Type | Required Testing |
| ----- | ----- |
| fix – Bug Fix | Regression test confirming fix, staging environment validation |
| feat – New feature refactor – Code restructuring chore – Maintenance build – Build tooling style – Formatting only perf – Performance improvements | Unit tests, integration tests, staging environment validation |
| infra \- Infrastructure revert – Undo changes | Staging environment validation |
| security \-- Security patch | Vulnerability scan after patch |
| ci – CI/CD changes | Pipeline validation (and staging environment validation if the change impacts deployment) |
| test – Test updates docs – Documentation | Standard PR review |
| mlmodel - changes to ML and AI models | model evaluation metrics are always documented, including bias/fairness check |


### Continuous Integration  
We use GitHub Actions for continuous integration. See [here](https://docs.github.com/en/actions) for GitHub's documentation.

You will know if any test breaks when you commit, and the tests will be run again in the continuous integration pipeline.

## Approval and Merging

### Merging to develop

1. Reviewer approves the GitHub pull request  
2. Developer updates the Asana task status to **"Ready to test"**  
3. Pull request is merged by the developer, reviewer, or a designated manager  
4. Once merged, code is automatically deployed to the staging environment for validation

### Merging to main / production

1. Reviewer approves the GitHub pull request  
2. Developer updates the Asana task status to **"Ready to Deploy"**  
3. Pull request is merged by the reviewer or a designated manager — **not the original author** (for Medium and High-risk changes)

## Versioning

Each release should be documented in the CHANGELOG as outlined in [Versioning & Release Management](https://datakind.atlassian.net/wiki/spaces/TT/pages/784793601/Versioning+Release+Management#Changelog-%26-Release-Notes).

Releases to `main` should be tagged with a semantic version number.

Semver format: **MAJOR.MINOR.BUGFIX**

- **MAJOR**: Breaking changes happen from one version to the next.  
- **MINOR**: Extends the existing code, but should be backwards compatible with old code.  
- **BUGFIX**: Doesn't add much new, but fixes issues along the way.
