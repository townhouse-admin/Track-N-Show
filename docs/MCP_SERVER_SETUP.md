# GitHub MCP Server Setup — TH-1 (townhouse-8gb-one)

> **Server:** townhouse-8gb-one | **IP (Tailscale):** 100.91.241.68 | **Port:** 3100
> **Datum:** 2026-04-16

---

## 🏗️ Arkitektur

```
Du (Tailscale-ansluten)
        │
        │ http://100.91.241.68:3100/sse
        ▼
┌─────────────────────────────────────────┐
│  TH-1 Server (100.91.241.68)            │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │  PM2 Process: github-mcp-server  │    │
│  │                                  │    │
│  │  supergateway (Node.js, :3100)   │    │
│  │     │ stdio-brygga               │    │
│  │     ▼                            │    │
│  │  Docker Container               │    │
│  │  ghcr.io/github/github-mcp-server│    │
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘
        │
        │ GitHub API
        ▼
  api.github.com
```

---

## 🚀 Installation

### Förutsättningar
- Ubuntu 24.04 LTS
- Docker installerat
- Node.js + npm installerat
- PM2 installerat globalt
- Supergateway installerat globalt

### Installationskommandon

```bash
# 1. Installera Docker
bash /root/get-docker.sh

# 2. Installera PM2 och supergateway
npm install -g pm2 supergateway

# 3. Dra hem Docker-imagen
docker pull ghcr.io/github/github-mcp-server

# 4. Skapa startskript
cat > /root/start-mcp.sh << 'EOF'
#!/bin/bash
export GITHUB_PERSONAL_ACCESS_TOKEN=<DIN_TOKEN_HÄR>
supergateway \
  --stdio 'docker run -i --rm -e GITHUB_PERSONAL_ACCESS_TOKEN ghcr.io/github/github-mcp-server' \
  --port 3100 \
  --baseUrl http://100.91.241.68:3100 \
  --ssePath /sse \
  --messagePath /message \
  --cors
EOF
chmod +x /root/start-mcp.sh

# 5. Starta med PM2
pm2 start /root/start-mcp.sh --name github-mcp-server
pm2 save
pm2 startup
```

---

## 🔌 Klientkonfiguration

### Claude Code (claude.json)
```json
{
  "mcpServers": {
    "github": {
      "type": "sse",
      "url": "http://100.91.241.68:3100/sse"
    }
  }
}
```

### VS Code (settings.json)
```json
{
  "mcp": {
    "servers": {
      "github-tailscale": {
        "type": "sse",
        "url": "http://100.91.241.68:3100/sse"
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
      "url": "http://100.91.241.68:3100/sse",
      "transport": "sse"
    }
  }
}
```

### Åtkomst-URL
```
SSE endpoint:  http://100.91.241.68:3100/sse
Message path:  http://100.91.241.68:3100/message
```

> ⚠️ **Kräver Tailscale-anslutning** — servern är inte åtkomlig från öppna internet

---

## 🛠️ Hantering

```bash
# Status
pm2 status

# Loggar
pm2 logs github-mcp-server

# Omstart
pm2 restart github-mcp-server

# Stopp
pm2 stop github-mcp-server
```

---

## 🧰 Tillgängliga MCP-verktyg

GitHub MCP-servern exponerar dessa verktygsgrupper:

| Toolset | Verktyg (urval) |
|---------|-----------------|
| **repos** | search_repositories, get_file_contents, create_or_update_file, push_files |
| **issues** | create_issue, list_issues, get_issue, update_issue, add_issue_comment |
| **pull_requests** | create_pull_request, list_pull_requests, merge_pull_request, get_pull_request |
| **code_security** | get_secret_scanning_alert, list_code_scanning_alerts |
| **actions** | list_workflows, trigger_workflow, get_workflow_run |
| **notifications** | list_notifications, mark_thread_as_read |

---

## 🔒 Säkerhetsnoteringar

- Token lagrad i miljövariabel (inte i klartext i konfig)
- Åtkomst begränsad till Tailscale-nätverket
- Byt token regelbundet via GitHub Settings → Personal Access Tokens
- Överväg `--read-only` flag för läs-only användning

---
*Senast uppdaterad: 2026-04-16*
