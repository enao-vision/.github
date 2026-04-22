# enao-vision/.github

Shared GitHub configuration and reusable workflows for the enao-vision organization.

## Reusable Workflows

Call these from any repo in the org using `workflow_call`.

### Claude Code Review

AI-powered PR review via [Claude Code Action](https://github.com/anthropics/claude-code-action).

```yaml
# .github/workflows/review.yml
name: Review

on:
  pull_request:

jobs:
  claude:
    uses: enao-vision/.github/.github/workflows/claude-review.yml@main
    secrets:
      anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
```

Requires `ANTHROPIC_API_KEY` set as an org-level secret.

### Dependency Review

Scans PRs for newly introduced vulnerable or license-restricted dependencies. Fails on `high` severity findings and posts a summary comment.

```yaml
# .github/workflows/dependency-review.yml
name: Dependency Review

on:
  pull_request:

jobs:
  deps:
    uses: enao-vision/.github/.github/workflows/dependency-review.yml@main
```

No secrets required — uses the built-in `GITHUB_TOKEN`.

## Org Secrets

| Secret | Used by |
|--------|---------|
| `ANTHROPIC_API_KEY` | `claude-review.yml` |
