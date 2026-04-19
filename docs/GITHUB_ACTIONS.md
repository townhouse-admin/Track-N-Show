# Top 10: GitHub Actions

> **Källor:** [sdras/awesome-actions](https://github.com/sdras/awesome-actions) + [anthropics/claude-code-action](https://github.com/anthropics/claude-code-action)

---

## TOP 10

| # | Namn | Kategori | Beskrivning |
|---|------|----------|-------------|
| 1 | claude-code-action | AI/CI | Claude Code i GitHub CI — PR-review, doc-uppdatering, CI-debugging |
| 2 | actions/checkout | Core | Checkar ut repot — alltid första steget |
| 3 | actions/cache | Performance | Cachar npm/pip/cargo för snabbare builds |
| 4 | docker/build-push-action | Deploy | Bygger och pushar Docker-images |
| 5 | codecov/codecov-action | Quality | Laddar upp code coverage till Codecov |
| 6 | github/codeql-action | Säkerhet | Statisk kodsäkerhetsanalys med CodeQL |
| 7 | slackapi/slack-github-action | Notifications | Skickar workflow-status till Slack |
| 8 | softprops/action-gh-release | Release | Skapar GitHub Releases med assets |
| 9 | actions/labeler | PR Auto | Auto-labela PRs baserat på ändrade filer |
| 10 | google-github-actions/deploy-cloudrun | Deploy | Deploya direkt till Google Cloud Run |

---

## claude-code-action Exempel

### Auto PR-review
```yaml
on:
  pull_request:
    types: [opened, synchronize]
jobs:
  claude-review:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
      contents: read
    steps:
      - uses: anthropics/claude-code-action@v1
        with:
          prompt: Review this PR for code quality and security.
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
```

### Auto doc-uppdatering
```yaml
on:
  pull_request:
    paths: ["src/api/**/*.ts"]
steps:
  - uses: anthropics/claude-code-action@v1
    with:
      prompt: Update README.md API docs to match changes in this PR.
      anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
```

---

*Senast uppdaterad: 2026-04-19*
