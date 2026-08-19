# `/archive-todos` — gerar afazeres pro overdev a partir do histórico recuperável

Objetivo: transformar o que o archive (+ git) guarda em um `.schematize/overdev/CHECKLIST.md` pronto
pra rodar sob o overdev. É a ponte "história → próximo trabalho".

## Fontes recuperáveis a varrer (exaustivo, por contagem)
- `<projeto>/_archive/overdev/CHECKLIST.md` (e o de `.schematize/`): todo `- [ ]` (aberto) e `- [~]`
  (on-hold/parkeado).
- `PERGUNTAS-OVERDEV.txt` + `premature-stops.log`: perguntas parkeadas sem resposta; paradas travadas.
- `<projeto>/_archive/decisoes/*`: ADRs `proposed` que nunca viraram accepted/rejected.
- `<projeto>/_archive/overdev/PLAN.md`: itens do plano sem prova de conclusão.
- `<projeto>/_archive/chats/*`: handoffs com seção ABERTO / "EM ABERTO" / "próximos passos".
- Histórico git: TODOs/FIXMEs introduzidos e não resolvidos; promessas em mensagens de commit.
- Qualquer `.md` do archive com `- [ ]`/`- [~]`/"EM ABERTO".

## Disciplina (red-first, da schematize-audit)
- **"Feito" sem prova volta a ABERTO.** Checkbox `- [x]` cujo teste/commit/arquivo/gate NÃO passa hoje
  vira `- [ ]` de novo. Suspeito ≠ feito.
- On-hold cuja pergunta ninguém respondeu = item aberto (com a pergunta anexada).
- ADR `proposed` eterno = item aberto (decidir accepted/rejected).

## Saída
1. Deriva o CHECKLIST exaustivo (1 item/linha, cada um com **como provar**), na convenção de 2 níveis
   (`- [ ]` máquina · `- [H ]` humano · `- [~]` on-hold), agrupado por origem.
2. Grava em `.schematize/overdev/CHECKLIST.md` (+ OBJETIVO.md com o alvo "sanear o histórico recuperado").
3. Espelha no `<projeto>/_archive/overdev/`.
4. Reporta a contagem por fonte e sugere `schematize overdev start "sanear archive"` (ou o botão) pra
   rodar sob a trava do overdev — o agente não para até fechar.

> Se quiser o VEREDITO formal (cobertura A/A + órfãos RED que travam), rode `/audit-run` depois.
