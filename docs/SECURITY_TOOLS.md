# Security Tools

> **Källor:** [Hack-with-Github/Awesome-Hacking](https://github.com/Hack-with-Github/Awesome-Hacking) · [OWASP/glue](https://github.com/OWASP/glue) · [indeedops/ShadowBuster](https://github.com/indeedops/ShadowBuster)

---

## TOP 10

| # | Namn | Kategori | Beskrivning | Länk |
|---|------|----------|-------------|------|
| 1 | OWASP Glue | Pipeline | Orchestreringsramverk för automatiserad säkerhetsanalys | [GitHub](https://github.com/OWASP/glue) |
| 2 | ShadowBuster | SOC | Realtidsvisualisering av säkerhetsevent på karta via WebSocket | [GitHub](https://github.com/indeedops/ShadowBuster) |
| 3 | SecLists | Pentesting | Samlingar för säkerhetstestning — lösenord, payloads, fuzzing | [GitHub](https://github.com/danielmiessler/SecLists) |
| 4 | PayloadsAllTheThings | Pentesting | Payload-samlingar för webb-säkerhetstestning och CTF | [GitHub](https://github.com/swisskyrepo/PayloadsAllTheThings) |
| 5 | API Security Checklist | API | Checklista för säkerhet vid API-design och release | [GitHub](https://github.com/shieldfy/API-Security-Checklist) |
| 6 | awesome-devsecops | DevSecOps | Kurerad lista med DevSecOps-verktyg för pipelines | [GitHub](https://github.com/devsecops/awesome-devsecops) |
| 7 | awesome-pentest | Pentesting | Komplett resurssamling för penetrationstestning | [GitHub](https://github.com/enaqx/awesome-pentest) |
| 8 | awesome-incident-response | IR | Verktyg och resurser för incident response | [GitHub](https://github.com/meirwah/awesome-incident-response) |
| 9 | cargo-audit | Rust | Skannar Rust-dependencies för kända CVEs | [GitHub](https://github.com/rustsec/rustsec) |
| 10 | ThreatHunter-Playbook | Threat Hunting | Spelbok för threat hunting-hypoteser och tekniker | [GitHub](https://github.com/Cyb3rWard0g/ThreatHunter-Playbook) |

---

## OWASP Glue Docker

```bash
docker pull owasp/glue
docker run -v /path/to/repo:/target owasp/glue --output json /target > results.json
```

---

*Senast uppdaterad: 2026-04-19*
