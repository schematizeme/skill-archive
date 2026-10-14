---
name: schematize-archive
metadata:
  version: 0.2.0
description: >-
  Rege o `<projeto>/<projeto>_archive/` obrigatório (repo git privado: overdev, índice, ADRs, chats, handoffs) e gera
  afazeres para o overdev a partir do histórico. Use ao iniciar/retomar projeto, fechar marco ou recuperar o que
  ficou aberto (`/archive-init`, `/archive-todos`).
---

# O ARCHIVE da casa (schematize-archive) — criticidade 0

Armazenar o histórico da evolução do sistema **NÃO é opcional**. O `<projeto>/<projeto>_archive/` é o rastro
**durável e recuperável** que responde, a qualquer momento, *o que foi decidido, planejado, feito, e o
que ficou aberto* — a **observabilidade da evolução**. Sem ele, o sistema é uma caixa-preta: cada
retomada recomeça do zero, promessas somem, "feito" não se prova. **Archive ausente = bug de
criticidade 0**, não um detalhe de fim de tarefa.

**Versão:** skill `schematize-archive` v0.2.0. Changelog em `CHANGELOG.md`.

## Piso inegociável
- **O archive é OBRIGATÓRIO** em todo projeto — materializado como `<projeto>/<projeto>_archive/`, **DENTRO do
  dir do projeto, irmão dos diretórios de microserviços** (não irmão do projeto). TUDO fica dentro do
  projeto. O motor `schematize overdev start` já o cria/espelha; sem archive, **criá-lo é o 1º item**.
- **O archive é um REPOSITÓRIO git PRÓPRIO, PRIVADO e obrigatório** — assim como os repos dos
  microserviços, mas sua função é a **evolução do projeto DOCUMENTADA**. Nasce com `git init`, tem
  **remote privado** (`<projeto>_archive`, private), e é **versionado por marco** (commit a cada
  decisão/plano/handoff/fechamento). NÃO é gitignored no projeto — é um repo, não lixo operacional.
  (O operacional volátil é o `.schematize/`, esse sim gitignored.)
- **O que MORA no archive** (durável, recuperável): `overdev/` (OBJETIVO, PLAN, DECISOES, CHECKLIST,
  NOTAS, premature-stops, AAAA-MM-DD-CONTEXTO.md), `index/` (MAPA + grafos §39), `decisoes/` (ADRs
  `ADR-NNNN-<slug>.md`, ciclo proposed→accepted/rejected), `chats/` (rastro bruto da sessão),
  `context/` (handoffs `AAAA-MM-DD-<slug>-context.md` — o FEITO-vs-ABERTO de cada sessão),
  `context_agent/` (contexto portável), `plan/`, `scan/`, `qa/`, `audit/`, `pentest/`,
  `orchestration/` e `scaffold/` (relatórios de cada skill). Planta completa em `references/archive.md`. O operacional vivo é `.schematize/`; o **espelho durável é o archive**.
- **Nada de histórico só na cabeça/no chat volátil.** Decisão tomada → grava no archive. Plano feito →
  archive. Sessão que fez handoff → archive. É o que a schematize-audit depois COBRA.

## Comandos
- **`/archive-init`** — materializa a estrutura obrigatória do `<projeto>/<projeto>_archive/` e checa o que falta
- **`/archive-check`** — o gate do archive: segredo/PII/binário/`.gitignore` interno/ADR duplicado/convenção de nome, com o procedimento de **recuperação** ensaiado ao lado (`scripts/check-archive.sh`)
  (nunca deixa o archive ausente). Ver `references/archive.md`.
- **`/archive-todos`** — o principal: **gera afazeres pro overdev a partir do histórico recuperável**.
  Varre o archive + git, enumera o ABERTO/prometido-e-não-provado, e deriva o
  `.schematize/overdev/CHECKLIST.md`. Ver `references/gerar-afazeres.md`.
- **`schematize archive`** (CLI/GUI) — POPULA o archive: extrai o chat da sessão pro `chats/` (cada mensagem = um item), gera o `context_agent/#N.txt` (contexto portável entre PCs/apps) e commita. É o que torna a disciplina EXECUTÁVEL (não manual).
- **`/archive-help`** — mapa da skill.

## Como se encaixa
- **schematize-engineering** (archive §28, overdev §0/§2, índice §39) — a BASE que exige o archive.
- **schematize-audit** — o oráculo dos órfãos RED: `/archive-todos` reusa a disciplina de "feito sem
  prova volta a aberto" e pode disparar `/audit-run` pra o veredito.
- **schematize-overdev-context** — a Fase 0: `/archive-todos` produz o insumo que a Fase 0 consome.
