# antonio-skills — Marketplace de Skills

Marketplace pessoal de **Agent Skills** (formato aberto `SKILL.md` — [agentskills.io](https://agentskills.io)), compatível com:

- **Claude Code** — instalação via `/plugin marketplace add` + `/plugin install`
- **AionUi** — fonte registrada no skills market (`custom-skill-paths.json`) → Configurações → Skills
- Qualquer outro cliente que consuma Agent Skills (Gemini CLI, OpenCode, Cursor, VS Code/Copilot, Goose...)

## Pacotes

| Plugin | Skills | Descrição |
|---|---|---|
| `frontend-design-pack` | 21 | Design frontend completo: UI/UX, tipografia, cores, acessibilidade, landing pages, padrões de componentes, auditoria — orquestrados por `webdesign-review` |
| `utilities-pack` | 7 | `antislop` (anti-clichê de IA: UI, código, copywriting, texto humano, layout mobile) + `owasp-reference` |

## Instalar no Claude Code

```
/plugin marketplace add fbabiato84/antonio-skills
/plugin install frontend-design-pack@antonio-skills
/plugin install utilities-pack@antonio-skills
```

Atualizar depois: `/plugin marketplace update antonio-skills`

## Instalar no AionUi

O repo está registrado como fonte do skills market nativo (`custom-skill-paths.json`):

```json
{ "name": "antonio-skills", "path": "https://github.com/fbabiato84/antonio-skills" }
```

Abra **Configurações → Skills** no AionUi para navegar e instalar pelo market, ou importe direto:
`aioncore config skills import` apontando para qualquer pasta de skill deste repo.

## Estrutura

```
.claude-plugin/marketplace.json   # catálogo do marketplace (padrão Claude Code)
<skill-name>/SKILL.md             # cada skill (spec Agent Skills)
<skill-name>/references/...       # material de apoio da skill
```

## Créditos

- Skills de design frontend adaptadas de [flitzrrr/frontend-design-skills](https://github.com/flitzrrr/frontend-design-skills) (spec [agentskills.io](https://agentskills.io))
- Formato de marketplace: `.claude-plugin/marketplace.json` ([docs Claude Code](https://code.claude.com/docs/en/plugins/create-marketplace.md))
