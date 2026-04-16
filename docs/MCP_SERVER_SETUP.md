# GitHub MCP Server Setup — TH-1

> **Stack:** Docker + supergateway + PM2
> **Transport:** SSE (Server-Sent Events)
> **Åtkomst:** Kräver Tailscale-anslutning

---

## 🏗️ Arkitektur

```
Du (Tailscale-ansluten)
        │
        │  SSE via Tailscale
        ▼
┌─────────────────────────────────────────┐
│  TH-1 Server                            │
│                                         │
│  PM2 → supergateway (Node.js)           │
│            │ stdio-brygga               │
│            ▼                            │
│  Docker: github-mcp-server              │
│            │                            │
└────────────┼────────────────────────────┘
             │ GitHub API
             ▼
       api.github.com
```

---

## 🚀 Installation

### Förutsättningar

```bash
# Docker
bash /root/get-docker.sh

# PM2 + supergateway
npm install -g pm2 supergateway

# Hämta Docker-imagen
docker pull ghcr.io/github/github-mcp-server
```

### Startskript (`/root/start-mcp.sh`)

```bash
#!/bin/bash
# Token läses från miljövariabel — commit ALDRIG token direkt
export GITHUB_PERSONAL_ACCESS_TOKEN="${GITHUB_PAT}"

supergateway \
  --stdio 'docker run -i --rm -e GITHUB_PERSONAL_ACCESS_TOKEN ghcr.io/github/github-mcp-server' \
  --port "${MCP_PORT}" \
  --baseUrl "http://${TH1_TAILSCALE_IP}:${MCP_PORT}" \
  --ssePath /sse \
  --messagePath /message \
  --cors
```

> Sätt `GITHUB_PAT`, `MCP_PORT` och `TH1_TAILSCALE_IP` i `/root/.env` — **inte** i skriptet.

### Starta med PM2

```bash
pm2 start /root/start-mcp.sh --name github-mcp-server
pm2 save
pm2 startup
```

---

## 🔌 Klientkonfiguration

> Ersätt `<TH1_TAILSCALE_IP>` och `<MCP_PORT>` med värden från intern wiki.

### Claude Code

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

### VS Code (`settings.json`)

```json
{
  "mcp": {
    "servers": {
      "github-tailscale": {
        "type": "sse",
        "url": "http://<TH1_TAILSCALE_IP>:<MCP_PORT>/sse"
      }
    }
  }
}
```

### Cursor / Windsurf

```json
{
  "mcpServers": {
    "github": {
      "url": "http://<TH1_TAILSCALE_IP>:<MCP_PORT>/sse",
      "transport": "sse"
    }
  }
}
```

---

## 🛠️ Hantering

```bash
pm2 status
pm2 logs github-mcp-server
pm2 restart github-mcp-server
pm2 stop github-mcp-server
```

---

## 🧰 Tillgängliga MCP-verktygsgrupper

| Toolset | Exempel på verktyg |
|---------|-------------------|
| **repos** | search_repositories, get_file_contents, push_files |
| **issues** | create_issue, list_issues, update_issue |
| **pull_requests** | create_pull_request, merge_pull_request |
| **code_security** | list_secret_scanning_alerts, list_code_scanning_alerts |
| **actions** | list_workflows, trigger_workflow, get_workflow_run |
| **notifications** | list_notifications, mark_thread_as_read |

---

## 🔒 Säkerhetsnoteringar

- Token lagras **aldrig** i klartext i skript eller konfig
- Åtkomst är begränsad till Tailscale-nätverket
- Rotera GitHub PAT regelbundet (Settings → Developer settings → PATs)
- Överväg `--read-only` för läs-only-scenarier

---

*Senast uppdaterad: 2026-04-16*
