---
description: Mapa da skill schematize-archive (o archive criticidade 0 + gerar afazeres do histórico).
---
**schematize-archive** — o archive da casa como CRITICIDADE 0.
- `/archive-init` — materializa o `<projeto>/<projeto>_archive/` obrigatório (nunca deixa ausente).
- `/archive-check` — varre o archive antes do commit (segredo, PII, binário, `.gitignore` interno, ADR duplicado, convenção de nome) e lembra o ensaio de recuperação. **Verde não é permissão para colar `.env`.**
- `/archive-todos` — GERA afazeres pro overdev a partir do histórico recuperável (o que ficou aberto).
- Pareia: schematize-engineering (archive §28), schematize-audit (órfãos RED), schematize-overdev-context (Fase 0).
