# Changelog — schematize-archive

## [0.1.1] — 2026-08-18
Archive fica DENTRO do projeto (`<projeto>/_archive/`, irmão dos microserviços) — não mais irmão do projeto.


## [0.1.0] — 2026-08-18
Skill nova: o archive como CRITICIDADE 0 (obrigatório, não opcional) + gerador de afazeres pro overdev.
### Adicionado
- Piso: `<projeto>/_archive/` obrigatório (checklists, planos, decisões/ADRs, chats/handoffs, índice, audit/pentest). Archive ausente = bug de observabilidade.
- `/archive-init` — materializa a estrutura do archive.
- `/archive-todos` — gera `.schematize/overdev/CHECKLIST.md` a partir do histórico recuperável do archive + git (itens abertos/prometidos-e-não-provados), com disciplina red-first da schematize-audit.
- `/archive-help`.
