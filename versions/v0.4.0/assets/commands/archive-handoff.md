---
description: schematize-archive — gera o handoff (context.md + checklist.md) no archive, sem compactar.
---
Gere o handoff em `<projeto>/<projeto>_archive/context/`: `AAAA-MM-DD-<slug>-context.md` (o que foi
feito, decisões, o que o `check-archive.sh` acusou, estado do archive e do remote privado) e
`AAAA-MM-DD-<slug>-checklist.md` (FEITO vs ABERTO, nas três classes da casa: `- [ ]` máquina ·
`- [H ]` humano · `- [~]` on-hold). Não compacte — só grave, commite e dê push no repo do archive.
Nunca grave segredo, `.env` ou PII no handoff.
