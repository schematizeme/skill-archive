---
description: GERA AFAZERES pro overdev a partir do histórico recuperável do archive (+ git) — deriva o .schematize/overdev/CHECKLIST.md do que ficou aberto/prometido-e-não-provado, com disciplina red-first.
argument-hint: "[escopo opcional]"
---
Gere os **afazeres do overdev a partir do histórico recuperável** seguindo `references/gerar-afazeres.md`.
Varra EXAUSTIVAMENTE o `<projeto>/_archive/` + `.schematize/` + histórico git: checklists com `- [ ]`/
`- [~]`, perguntas parkeadas (`PERGUNTAS-OVERDEV.txt`), premature-stops, ADRs `proposed`, planos com
itens abertos, handoffs de `chats/` com seção EM ABERTO, TODOs/FIXMEs do git. Aplique a disciplina
red-first (**"feito" sem prova volta a ABERTO**; on-hold sem resposta = aberto). Derive um CHECKLIST
exaustivo (1 item/linha, cada um com COMO PROVAR, convenção de 2 níveis) agrupado por origem, grave em
`.schematize/overdev/CHECKLIST.md` (+ OBJETIVO.md + espelho no archive) e reporte a contagem por fonte.
Se o archive não existir, rode `/archive-init` primeiro (criticidade 0). Sugira rodar sob o overdev
(`schematize overdev start` / o botão) — o agente não para até fechar. Veredito formal? `/audit-run`.
