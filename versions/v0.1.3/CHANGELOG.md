# Changelog — schematize-archive

## [0.1.3] — 2026-08-18
Estrutura ganha `context_agent/` (contexto portável #N.txt). Comando `schematize archive` popula chats/ (transcript da sessão, 1 item/mensagem) + gera context_agent/#N.txt + commita. Disciplina executável, não manual.


## [0.1.2] — 2026-08-18
Archive é `<projeto>/<projeto>_archive/` — nome do projeto (prefixo comum dos microserviços) no dir, pra não misturar archives de projetos diferentes.


## [0.1.1] — 2026-08-18
Archive fica DENTRO do projeto (`<projeto>/<projeto>_archive/`, irmão dos microserviços) — não mais irmão do projeto.


## [0.1.0] — 2026-08-18
Skill nova: o archive como CRITICIDADE 0 (obrigatório, não opcional) + gerador de afazeres pro overdev.
### Adicionado
- Piso: `<projeto>/<projeto>_archive/` obrigatório (checklists, planos, decisões/ADRs, chats/handoffs, índice, audit/pentest). Archive ausente = bug de observabilidade.
- `/archive-init` — materializa a estrutura do archive.
- `/archive-todos` — gera `.schematize/overdev/CHECKLIST.md` a partir do histórico recuperável do archive + git (itens abertos/prometidos-e-não-provados), com disciplina red-first da schematize-audit.
- `/archive-help`.
