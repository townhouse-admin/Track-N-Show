# Server Map: TH-1 (townhouse-8gb-one)

> ⚠️ **Säkerhetsnotering:** IPs, portnummer och sökvägar utelämnas medvetet.
> Detaljer finns i intern wiki (åtkomst kräver Tailscale).

**Datum:** 2026-04-16
**Hostname:** townhouse-8gb-one

---

## 1. System Overview

| Egenskap | Värde |
|----------|-------|
| OS | Ubuntu 24.04.4 LTS (Noble Numbat) |
| Provider | Hetzner (vServer) |
| Virtualisering | KVM |
| Arkitektur | x86_64 |

---

## 2. Hardware Specs

| Komponent | Spec |
|-----------|------|
| CPU | 4 vCPUs |
| RAM | 8 GB |
| Disk | 80 GB |

---

## 3. Nätverk

- Ansluten till **Tailscale**-nätverket (4 aktiva noder)
- Reverse proxy via **Caddy**
- Nätverksdetaljer (IPs, portar) — se intern wiki

---

## 4. Tjänster & Applikationer

### god-tool (Dashboard)
- **Stack:** Node.js (Express), React (Vite), Socket.io, Tailscale SDK
- **Process manager:** PM2
- **Proxy:** Caddy

### github-mcp-server
- **Stack:** Docker + supergateway (SSE-brygga)
- **Process manager:** PM2
- **Transport:** SSE (Server-Sent Events)
- **Åtkomst:** Tailscale-nätverket

### Caddy
- **Funktion:** Reverse proxy mot god-tool

---

## 5. PM2-processer

| Namn | Status |
|------|--------|
| god-tool | online |
| github-mcp-server | online |

---

## 6. Infrastrukturkomponenter

Installerat/konfigurerat på servern:

- Docker (container runtime)
- PM2 (process manager)
- Caddy (reverse proxy)
- Tailscale (nätverksanslutning)
- Node.js + npm

---

## 7. Rekommendationer

- Sätt upp HTTPS via Caddy (certifikat saknas för nuvarande)
- Undvik att köra tjänster som `root` — skapa dedikerade användare
- Rotera GitHub PAT regelbundet
- Aktivera UFW-loggar

---

*Rapport senast uppdaterad: 2026-04-16*
