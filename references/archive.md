# O `<projeto>_archive/` — estrutura obrigatória (criticidade 0)

Irmão do dir do projeto: `<parent>/<nome>_archive/`. O motor `schematize overdev start` já cria e
espelha `overdev/`. Se o projeto não tem archive, **criá-lo é o 1º item** — nunca siga sem archive.

## Estrutura
```
<projeto>_archive/
  overdev/     # OBJETIVO.md, PLAN.md, DECISOES.md, CHECKLIST.md, NOTAS.md, premature-stops.log
  index/       # MAPA.md + INDEX_GLOBAL.md + INDEX_FUNCTIONS.md + grafos (§39)
  decisoes/    # ADRs no ciclo proposed → accepted/rejected (uma decisão = um arquivo datado)
  chats/       # handoffs de contexto por sessão: FEITO-vs-ABERTO (o rastro do que cada sessão fez)
  audit/       # relatórios da schematize-audit
  pentest/     # relatórios da schematize-pentest
```
O operacional VIVO fica em `.schematize/` (overdev/, grafos/); o **espelho durável é o archive** — é
dele que a auditoria, a retomada e o `/archive-todos` recuperam a história.

## `/archive-init` — o que faz
1. Detecta/deriva `<projeto>_archive/` (irmão do projeto). Cria a estrutura acima se faltar.
2. Espelha o que já existe em `.schematize/` (overdev, grafos) pro archive.
3. Grava um handoff mínimo em `chats/` da sessão atual (o que foi feito, o que ficou aberto).
4. Reporta o que estava AUSENTE (o gap de observabilidade que acabou de ser fechado).

Regra: **nada de histórico volátil.** Toda decisão/plano/handoff relevante vira arquivo no archive.
