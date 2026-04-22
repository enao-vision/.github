# enao-vision/.github

Shared GitHub configuration and reusable workflows for the enao-vision organization.

## Usage

Each repo needs one caller file. All checks run in parallel on every PR:

```yaml
# each-repo → .github/workflows/pr-checks.yml
name: PR Checks

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  checks:
    uses: enao-vision/.github/.github/workflows/pr-checks.yml@main
    secrets: inherit
```

Secrets are set once at the org level and inherited automatically — no per-repo secret configuration needed. To add a new check org-wide, update [`workflows/pr-checks.yml`](workflows/pr-checks.yml) — no changes needed in individual repos.

## Workflows

| Workflow | Description |
|----------|-------------|
| [`pr-checks.yml`](workflows/pr-checks.yml) | Orchestrator — calls all checks below |
| [`claude-review.yml`](workflows/claude-review.yml) | AI-powered PR review via Claude |
| [`dependency-review.yml`](workflows/dependency-review.yml) | Flags vulnerable/license-restricted dependencies |
| [`release-notes-preview.yml`](workflows/release-notes-preview.yml) | Claude comments a release notes preview for PRs targeting main |

## Org Secrets

| Secret | Used by |
|--------|---------|
| `ANTHROPIC_API_KEY` | `claude-review.yml` |
