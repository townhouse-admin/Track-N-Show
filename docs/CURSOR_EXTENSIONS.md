# Cursor / VS Code Extensions

> **Källa:** [viatsko/awesome-vscode](https://github.com/viatsko/awesome-vscode)
> **Urval:** Top 10 för web development, DevOps och säkerhet — alla installerade 2026-04-19

---

## Installerade (2026-04-19)

| # | Namn | Extension ID | Kategori | Beskrivning |
|---|------|-------------|----------|-------------|
| 1 | GitLens | `eamodio.gitlens` | Git | Inline Git blame, commit-historik och repo-visualisering |
| 2 | Error Lens | `usernamehw.errorlens` | DX | Visar fel och varningar inline på raden |
| 3 | REST Client | `humao.rest-client` | API | Skicka HTTP-requests direkt i editorn |
| 4 | Docker | `ms-azuretools.vscode-docker` | DevOps | Syntax highlighting och container-hantering |
| 5 | Terraform | `hashicorp.terraform` | IaC | Syntax, linting, formatering och validering |
| 6 | Prettier | `esbenp.prettier-vscode` | Formatering | Automatisk kodformatering för JS/TS/CSS/HTML |
| 7 | ESLint | `dbaeumer.vscode-eslint` | Linting | JavaScript/TypeScript linting med auto-fix |
| 8 | Code Spell Checker | `streetsidesoftware.code-spell-checker` | Kvalitet | Stavningskontroll i kod och kommentarer |
| 9 | Thunder Client | `rangav.vscode-thunder-client` | API | REST/GraphQL API-testning med UI |
| 10 | Remote SSH | `ms-vscode-remote.remote-ssh` | Remote | Editera kod direkt på fjärrservrar via SSH |

---

## Snabbinstallation

```bash
CODE="/c/Users/Demo/AppData/Local/Programs/cursor/resources/app/bin/code"
for ext in eamodio.gitlens usernamehw.errorlens humao.rest-client \
  ms-azuretools.vscode-docker hashicorp.terraform esbenp.prettier-vscode \
  dbaeumer.vscode-eslint streetsidesoftware.code-spell-checker \
  rangav.vscode-thunder-client ms-vscode-remote.remote-ssh; do
  "$CODE" --install-extension "$ext" --force
done
```

---

*Senast uppdaterad: 2026-04-19*
