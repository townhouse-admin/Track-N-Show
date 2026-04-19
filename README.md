# Track-N-Show: TH-1 Infrastructure & AI Toolkit Map

> **Syfte:** Dokumentera TH-1-servern och ett kurerat AI-verktygsbibliotek.
> Känsliga detaljer (IPs, portar, tokens) förvaras **aldrig** i detta repo — se intern wiki.

---

## Innehållsförteckning

### Infrastruktur

| Dokument | Beskrivning |
|----------|-------------|
| [SERVER_MAP_TH1.md](./SERVER_MAP_TH1.md) | Serverkartering för TH-1 (desensitiserad) |
| [docs/MCP_SERVER_SETUP.md](./docs/MCP_SERVER_SETUP.md) | GitHub MCP Server setup via Tailscale |
| [docs/MCP_HUB_ARCHITECTURE.md](./docs/MCP_HUB_ARCHITECTURE.md) | MCP Hub-arkitektur och aggregering |

### AI & Agenter

| Dokument | Beskrivning |
|----------|-------------|
| [docs/AWESOME_AGENTS_TOP20.md](./docs/AWESOME_AGENTS_TOP20.md) | Top 20: AI Agent frameworks |
| [docs/MCP_SERVERS_TOP20.md](./docs/MCP_SERVERS_TOP20.md) | Top 20: MCP Servers |
| [docs/CLAUDE_CODE_TOOLS.md](./docs/CLAUDE_CODE_TOOLS.md) | Claude Code ekosystem — skills, hooks, CLI-verktyg |

### Copilot

| Dokument | Beskrivning |
|----------|-------------|
| [docs/COPILOT_HOOKS.md](./docs/COPILOT_HOOKS.md) | Alla 6 Copilot Hooks |
| [docs/COPILOT_PLUGINS_TOP20.md](./docs/COPILOT_PLUGINS_TOP20.md) | Top 20: Copilot Plugins |
| [docs/COPILOT_SKILLS_TOP20.md](./docs/COPILOT_SKILLS_TOP20.md) | Top 20: Copilot Skills |
| [docs/COPILOT_INSTRUCTIONS_TOP20.md](./docs/COPILOT_INSTRUCTIONS_TOP20.md) | Top 20: Copilot Instructions |
| [docs/COPILOT_AGENTS_TOP20.md](./docs/COPILOT_AGENTS_TOP20.md) | Top 20: Copilot Agents |

### DevOps & Cloud

| Dokument | Beskrivning |
|----------|-------------|
| [docs/AZURE_DEVOPS_TOP20.md](./docs/AZURE_DEVOPS_TOP20.md) | Top 20: Azure DevOps resurser |
| [docs/GITHUB_ACTIONS.md](./docs/GITHUB_ACTIONS.md) | Top 10: GitHub Actions inkl. claude-code-action |
| [docs/SYSADMIN_TOOLS.md](./docs/SYSADMIN_TOOLS.md) | Top 10: Sysadmin-verktyg (Prometheus, Ansible, Restic...) |
| [docs/CURSOR_EXTENSIONS.md](./docs/CURSOR_EXTENSIONS.md) | Top 10: Cursor/VS Code extensions |
| [docs/RUST_CLI_TOOLS.md](./docs/RUST_CLI_TOOLS.md) | Top 10: Rust CLI-verktyg (ripgrep, bat, eza...) |

### Säkerhet

| Dokument | Beskrivning |
|----------|-------------|
| [docs/SECURITY_TOOLS.md](./docs/SECURITY_TOOLS.md) | Top 10: Säkerhetsverktyg (OWASP, SecLists, ShadowBuster...) |

---

## Serveröversikt (TH-1)

```
┌────────────────────────────────────────────────────────────┐
│                    TH-1 (townhouse-8gb-one)                 │
│                   Hetzner vServer — Ubuntu 24.04            │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌─────────────────┐  │
│  │   Caddy      │  │  god-tool    │  │ github-mcp-     │  │
│  │  HTTP proxy  │  │  Dashboard   │  │ server (SSE)    │  │
│  │  (port fwd)  │  │  Node.js/PM2 │  │ Docker/PM2      │  │
│  └──────────────┘  └──────────────┘  └─────────────────┘  │
│                                                             │
│  Tailscale-nätverket: 4 aktiva noder                        │
│  (se intern wiki för IP-detaljer)                           │
└────────────────────────────────────────────────────────────┘
```

---

## AI Toolkit Stack (Kurerat)

### Aktiva tjänster på TH-1

| Service | Åtkomst | Status |
|---------|---------|--------|
| GitHub MCP Server (SSE) | Via Tailscale — se intern wiki | Online |
| God-Tool Dashboard | Via Tailscale — se intern wiki | Online |

### Resources per kategori

```
AI Agents        ──────► 20 agenter   [docs/AWESOME_AGENTS_TOP20.md]
MCP Servers      ──────► 20 servrar   [docs/MCP_SERVERS_TOP20.md]
Claude Code      ──────► 20+ verktyg  [docs/CLAUDE_CODE_TOOLS.md]
Copilot Hooks    ──────►  6 hooks     [docs/COPILOT_HOOKS.md]
Copilot Plugins  ──────► 20 plugins   [docs/COPILOT_PLUGINS_TOP20.md]
Copilot Skills   ──────► 20 skills    [docs/COPILOT_SKILLS_TOP20.md]
Copilot Instr.   ──────► 20 instr.    [docs/COPILOT_INSTRUCTIONS_TOP20.md]
Copilot Agents   ──────► 20 agenter   [docs/COPILOT_AGENTS_TOP20.md]
Azure DevOps     ──────► 20 resurser  [docs/AZURE_DEVOPS_TOP20.md]
GitHub Actions   ──────► 10 actions   [docs/GITHUB_ACTIONS.md]
Sysadmin Tools   ──────► 10 verktyg   [docs/SYSADMIN_TOOLS.md]
Cursor Ext.      ──────► 10 extensions[docs/CURSOR_EXTENSIONS.md]
Rust CLI Tools   ──────► 10 verktyg   [docs/RUST_CLI_TOOLS.md]
Security Tools   ──────► 10 verktyg   [docs/SECURITY_TOOLS.md]
```

---

## MCP Server Snabbstart

```json
{
  "mcpServers": {
    "github": {
      "type": "sse",
      "url": "http://<TH1_TAILSCALE_IP>:<MCP_PORT>/sse"
    }
  }
}
```

> Hämta `<TH1_TAILSCALE_IP>` och `<MCP_PORT>` från intern wiki.

Se [docs/MCP_SERVER_SETUP.md](./docs/MCP_SERVER_SETUP.md) för fullständig setup-guide.

---

## Säkerhetspolicy för detta repo

- **Inga IPs** — varken publika eller privata/Tailscale
- **Inga portar** — använd tjänstnamn istället
- **Inga tokens/credentials** — inte ens i kommentarer
- **Inga sökvägar** — inga absoluta filsystemsökvägar
- **Inga nodnamn** — Tailscale-nodnamn är interna

Brott mot ovanstående fångas automatiskt av [`.github/workflows/secret-scan.yml`](./.github/workflows/secret-scan.yml).

---

*Senast uppdaterad: 2026-04-19*
