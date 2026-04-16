# MCP Hub Arkitektur: Line 0 / Line 1

> **Plats:** `/opt/mcp-hub/` på TH-1
> **Port:** Tillgänglig via Tailscale — se intern wiki
> **Process manager:** PM2 (`mcp-line0-hub`)

---

## Arkitektur

```
Claude Code (du)
      │
      │  SSE via Tailscale
      ▼
┌─────────────────────────────────────────────────────────┐
│               MCP LINE 0 — Hub (port 3200)               │
│                   /opt/mcp-hub/line0/hub.js              │
│                                                          │
│  Verktyg:                                                │
│  • hub_status      — Visa status för alla anslutningar   │
│  • list_domains    — Lista alla 10 domäner               │
│  • query_domain    — Fråga en specifik domän             │
│  • search_all      — Sök parallellt i alla domäner       │
│  • get_domain_info — Metadata om en domän                │
└──────────────┬──────────────────────────────────────────┘
               │  stdio (10 parallella processer)
               ▼
┌──────────────────────────────────────────────────────────┐
│              MCP LINE 1 — 10 Domänservrar                 │
│              /opt/mcp-hub/line1/                          │
│                                                          │
│  ID                       Fil                            │
│  ─────────────────────────────────────────────────────── │
│  server-map               1-server-map.js                │
│  mcp-setup                2-mcp-setup.js                 │
│  azure-devops             3-azure-devops.js              │
│  awesome-agents           4-awesome-agents.js            │
│  mcp-servers              5-mcp-servers.js               │
│  copilot-hooks            6-copilot-hooks.js             │
│  copilot-plugins          7-copilot-plugins.js           │
│  copilot-skills           8-copilot-skills.js            │
│  copilot-instructions     9-copilot-instructions.js      │
│  copilot-agents           10-copilot-agents.js           │
│                                                          │
│  Verktyg per domän:                                      │
│  • list_items  — Lista alla objekt (max 20)              │
│  • get_item    — Hämta objekt #N                         │
│  • search      — Sök med nyckelord                       │
│  • get_info    — Metadata om servern och källan          │
└──────────────────────────────────────────────────────────┘
               │
               │  HTTPS (fetch vid behov, cachat)
               ▼
  raw.githubusercontent.com/townhouse-admin/Track-N-Show/main/
```

---

## Filstruktur

```
/opt/mcp-hub/
├── package.json              # ES modules, @modelcontextprotocol/sdk
├── shared/
│   └── base-line1-server.js  # Delad bas: fetch + markdown-parser + MCP-server
├── line0/
│   └── hub.js                # Line 0: Proxy-hub, ansluter till alla Line 1
└── line1/
    ├── 1-server-map.js
    ├── 2-mcp-setup.js
    ├── 3-azure-devops.js
    ├── 4-awesome-agents.js
    ├── 5-mcp-servers.js
    ├── 6-copilot-hooks.js
    ├── 7-copilot-plugins.js
    ├── 8-copilot-skills.js
    ├── 9-copilot-instructions.js
    └── 10-copilot-agents.js
```

---

## Användning — Exempelanrop

### Visa hubstatus
```
Verktyg: hub_status
Args: {}
```

### Lista alla domäner
```
Verktyg: list_domains
Args: {}
```

### Fråga en specifik domän
```
Verktyg: query_domain
Args: {
  "domain_id": "azure-devops",
  "tool": "list_items"
}
```

### Hämta item #5 från MCP Servers
```
Verktyg: query_domain
Args: {
  "domain_id": "mcp-servers",
  "tool": "get_item",
  "args": { "number": 5 }
}
```

### Sök i alla domäner parallellt
```
Verktyg: search_all
Args: { "query": "docker" }
```

---

## PM2-hantering

```bash
pm2 status                         # Visa alla processer
pm2 logs mcp-line0-hub             # Loggar för hubben
pm2 restart mcp-line0-hub          # Omstart
```

---

## Datakällor per domän

| Line-1 ID | Titel | GitHub-källa |
|-----------|-------|--------------|
| server-map | Server Map TH-1 | townhouse-admin/Track-N-Show |
| mcp-setup | MCP Server Setup | townhouse-admin/Track-N-Show |
| azure-devops | Azure DevOps Top 20 | johnlokerse/awesome-azure-devops |
| awesome-agents | Awesome Agents Top 20 | kyrolabs/awesome-agents |
| mcp-servers | MCP Servers Top 20 | punkpeye/awesome-mcp-servers |
| copilot-hooks | Copilot Hooks | awesome-copilot.github.com |
| copilot-plugins | Copilot Plugins Top 20 | awesome-copilot.github.com |
| copilot-skills | Copilot Skills Top 20 | awesome-copilot.github.com |
| copilot-instructions | Copilot Instructions Top 20 | awesome-copilot.github.com |
| copilot-agents | Copilot Agents Top 20 | awesome-copilot.github.com |

---

## Teknisk stack

| Komponent | Teknologi |
|-----------|-----------|
| Hub-server (Line 0) | Node.js ES modules, `@modelcontextprotocol/sdk` |
| Domänservrar (Line 1) | Node.js ES modules, `@modelcontextprotocol/sdk` |
| SSE-brygga | supergateway |
| Process manager | PM2 |
| Datatransport hub→domän | stdio (StdioClientTransport) |
| Datatransport klient→hub | SSE (Server-Sent Events) |
| Datakälla | GitHub raw (fetch, cachat per session) |

---
*Senast uppdaterad: 2026-04-16*
