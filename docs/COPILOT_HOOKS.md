# Awesome Copilot: Hooks (Alla 6)

> **Källa:** [awesome-copilot.github.com/hooks](https://awesome-copilot.github.com/hooks/)
> **Notering:** Endast 6 hooks finns tillgängliga — alla inkluderas

Hooks är shell-kommandon som körs automatiskt vid GitHub Copilot coding agent-events (session start/stop, tool calls etc.)

---

## 🏆 ALLA 6 HOOKS

| # | Namn | Trigger | Beskrivning | Länk |
|---|------|---------|-------------|------|
| 1 | **Dependency License Checker** | Session End | Skannar nyligen tillagda dependencies för licensefterlevnad (GPL, AGPL etc.) | [🔗](https://github.com/github/awesome-copilot/blob/main/hooks/dependency-license-checker) |
| 2 | **Governance Audit** | Prompt | Skannar agent-prompts för hotsignaler och loggar governance-events | [🔗](https://github.com/github/awesome-copilot/blob/main/hooks/governance-audit) |
| 3 | **Secrets Scanner** | Session End | Skannar modifierade filer för läckta hemligheter, credentials och känslig data | [🔗](https://github.com/github/awesome-copilot/blob/main/hooks/secrets-scanner) |
| 4 | **Session Auto-Commit** | Session End | Automatiskt commit + push när coding agent-session avslutas | [🔗](https://github.com/github/awesome-copilot/blob/main/hooks/session-auto-commit) |
| 5 | **Session Logger** | All Events | Loggar all coding agent-aktivitet för audit och analys | [🔗](https://github.com/github/awesome-copilot/blob/main/hooks/session-logger) |
| 6 | **Tool Guardian** | Pre-Tool | Blockerar farliga verktygsoperationer (destructive file ops, force push, DB drops) | [🔗](https://github.com/github/awesome-copilot/blob/main/hooks/tool-guardian) |

---

## 🔧 Hook-livscykeln

```
Session Start
    │
    ▼
[Governance Audit Hook] ──► Granska prompt för hot
    │
    ▼
Agent Arbetar...
    │
    ├─► [Tool Guardian Hook] ──► Blockera farliga operationer BEFORE execution
    │
    ▼
Session End
    │
    ├─► [Secrets Scanner Hook] ──► Skanna för läckta hemligheter
    ├─► [Dependency License Checker] ──► Kontrollera licensefterlevnad
    └─► [Session Auto-Commit] ──► Automatisk commit+push
    
Löpande: [Session Logger] ──► Loggar ALL aktivitet
```

---

## ⭐ Rekommenderad Konfiguration för Claude Code

```jsonc
// .claude/settings.json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "bash /path/to/secrets-scanner"
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "bash /path/to/dependency-license-checker"
          },
          {
            "type": "command",
            "command": "bash /path/to/session-logger"
          }
        ]
      }
    ]
  }
}
```

---
*Senast uppdaterad: 2026-04-16*
