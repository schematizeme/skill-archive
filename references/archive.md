# O `<projeto>/<projeto>_archive/` — estrutura obrigatória (criticidade 0)

DENTRO do dir do projeto: `<projeto>/<projeto>_archive/` — **irmão dos diretórios de microserviços** (não irmão do projeto). TUDO fica dentro do projeto. O `<projeto>` é o NOME DO PROJETO — o prefixo comum dos microserviços (`<projeto>_<microservice>`, ex.: `schematize_cli_rs`/`schematizeskills_api_rs` → `schematize`) — pra o archive nunca misturar com o de outro projeto. O motor `schematize overdev start` já cria e
espelha `overdev/`. Se o projeto não tem archive, **criá-lo é o 1º item** — nunca siga sem archive.

## Estrutura — a planta CANÔNICA (esta skill é a dona; as outras apontam para cá)

> Até 2026-08-21 havia **três plantas concorrentes** no catálogo (aqui, em
> `schematize-docs/references/indice-diagramas.md` e em `schematize-scaffold`), cada uma com um
> conjunto de pastas diferente — e **quatro caminhos de ADR** distintos, o que tornava o piso
> *"ADR `proposed` é órfão RED"* inexequível por construção: o `/docs-adr` gravava num lugar, a
> `/archive-todos` procurava noutro e a `/audit-run` num terceiro (achado B2/B2b). Esta é a planta
> única; qualquer outra citação do catálogo é **ponteiro para cá**, nunca uma segunda definição.

```
<projeto>/<projeto>_archive/
  overdev/     # OBJETIVO.md, PLAN.md, DECISOES.md, CHECKLIST.md, NOTAS.md,
               #   premature-stops.log, PERGUNTAS-OVERDEV.txt
  index/       # MAPA.md + INDEX_GLOBAL.md + INDEX_FUNCTIONS.md + grafos (§39)
  decisoes/    # ADRs no ciclo proposed -> accepted/rejected (uma decisão = um arquivo datado).
               #   CAMINHO ÚNICO de ADR da casa: quem grava (/docs-adr), quem lê (/archive-todos)
               #   e quem audita (/audit-run) usam ESTE. Nada de `docs/adr/` nem `archive/adr/`.
  chats/       # rastro BRUTO da sessão: cada mensagem extraída pelo `schematize archive`
  context/     # handoffs RICOS de contexto: os pares context.md + checklist.md (FEITO-vs-ABERTO)
               #   gravados por `/<slug>-cc` e `/<slug>-handoff` (70 ocorrências no catálogo)
  plan/        # planos do /eng-plan (fases + DoD + checklist)
  scan/        # achados do /eng-scan
  qa/          # planos e relatórios do Q.A. plan-first (/qa-plan, /qa-run)
  audit/       # relatórios da schematize-audit
  pentest/     # relatórios da schematize-pentest
```

> **`chats/` e `context/` são os DOIS lugares do rastro de sessão, e os dois são recuperáveis.**
> A distinção: `chats/` é o bruto (mensagem a mensagem, gerado por máquina); `context/` é o handoff
> escrito pelo modelo, com FEITO-vs-ABERTO. Até 2026-08-21 a planta listava só `chats/` enquanto
> todos os comandos `-cc`/`-handoff` gravavam em `context/` — e a `/archive-todos`, que varria só
> `chats/`, **devolvia vazio sem erro** (achado B1). Quem lê história tem de varrer **os dois**.
O operacional VIVO fica em `.schematize/` (overdev/, grafos/); o **espelho durável é o archive** — é
dele que a auditoria, a retomada e o `/archive-todos` recuperam a história.

## O archive é um REPOSITÓRIO git PRÓPRIO (privado, obrigatório)
Não é uma pasta solta nem lixo gitignored: é um **repo git como os dos microserviços**, cuja função é
a **evolução do projeto DOCUMENTADA**.
- **`git init`** no `<projeto>_archive/` (o motor faz no `overdev start`; o `/archive-init` garante).
- **Remote PRIVADO** obrigatório: `<projeto>_archive` (visibilidade **private** — histórico interno,
  nunca público). Ex.: `gh repo create <org>/<projeto>_archive --private`.
- **Versionado por marco:** commit a cada decisão/plano/handoff/fechamento (a mensagem conta a
  evolução). É o `git log` do archive que responde "como o sistema evoluiu".
- **NÃO é gitignored** no projeto (é um repo). O que É gitignored é o `.schematize/` (operacional volátil).

## Populado AUTOMATICAMENTE: `schematize archive`
O archive não é opcional NEM manual: rode **`schematize archive`** (ou o botão na GUI) — ele
materializa a estrutura, **extrai CADA mensagem** (você + respostas) do transcript da sessão pro
`chats/<sessão>.md` (um item por mensagem), gera o próximo **`context_agent/#N.txt`** (o contexto
portável) e **commita** no repo do archive. Rode ao fechar um marco, ao migrar de PC/app, ou sempre
que quiser um snapshot. Disciplina: **cada mensagem → item em `chats/`; cada checklist → itens no
CHECKLIST; cada decisão → arquivo em `decisoes/`**. Nada de histórico volátil.

## `/archive-init` — o que faz
1. Detecta/deriva `<projeto>/<projeto>_archive/` (irmão dos microserviços, dentro do projeto). Cria a estrutura acima se faltar.
2. **`git init`** o `<projeto>_archive/` se ainda não for repo; garante o remote **privado** `<projeto>_archive`.
3. Espelha o que já existe em `.schematize/` (overdev, grafos) pro archive.
4. Grava um handoff mínimo em `chats/` da sessão atual (o que foi feito, o que ficou aberto).
5. Reporta o que estava AUSENTE (o gap de observabilidade que acabou de ser fechado).

Regra: **nada de histórico volátil.** Toda decisão/plano/handoff relevante vira arquivo no archive.
