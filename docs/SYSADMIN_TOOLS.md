# Top 10: Sysadmin Tools

> **Källa:** [awesome-foss/awesome-sysadmin](https://github.com/awesome-foss/awesome-sysadmin)

---

## TOP 10

| # | Namn | Kategori | Beskrivning | Install |
|---|------|----------|-------------|--------|
| 1 | Prometheus | Monitoring | Metrics-insamling och time series DB | `docker run prom/prometheus` |
| 2 | Grafana | Visualisering | Dashboard för Prometheus, Loki, InfluxDB | `docker run grafana/grafana` |
| 3 | Ansible | Automation | Agentlös orkestrering för serverprovisionering | `pip install ansible` |
| 4 | Restic | Backup | Snabb, krypterad och verifierbar backup | `apt install restic` |
| 5 | Authentik | Identity | Self-hosted IdP — OAuth 2.0, SAML, LDAP | `docker compose up` |
| 6 | BorgBackup | Backup | Dedupliserande backup med stark kryptering | `apt install borgbackup` |
| 7 | Podman | Container | Daemonless container-engine, rootless Docker-ersättning | `apt install podman` |
| 8 | Loki | Logging | Grafana-kompatibel log-aggregering | `docker run grafana/loki` |
| 9 | Netdata | Monitoring | Realtids-monitoring med noll-konfiguration | `bash <(curl -s netdata.cloud/install)` |
| 10 | Fail2Ban | Säkerhet | Blockar IP:er vid upprepade misslyckade inloggningar | `apt install fail2ban` |

---

## Prometheus + Grafana Docker Compose

```yaml
services:
  prometheus:
    image: prom/prometheus:latest
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"
  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    depends_on:
      - prometheus
```

---

*Senast uppdaterad: 2026-04-19*
