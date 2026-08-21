---
description: Materializa o <projeto>/<projeto>_archive/ OBRIGATÓRIO (criticidade 0) — cria a estrutura, espelha o .schematize/ e grava o handoff da sessão; reporta o que estava ausente.
---
Materialize o **`<projeto>/<projeto>_archive/`** (irmão do projeto) seguindo `references/archive.md`. Archive é
**CRITICIDADE 0 — não opcional**. Passos: (1) crie a estrutura (`overdev/ index/ decisoes/ chats/
context/ audit/ pentest/`) se faltar — **`context/` junto de `chats/`**, que é onde os comandos
`/<slug>-cc` e `/<slug>-handoff` gravam e onde a `/archive-todos` também lê; (2) espelhe o operacional vivo de `.schematize/` (overdev, grafos) pro
archive; (3) grave o handoff da sessão atual (FEITO / EM ABERTO) em `context/<data>-<slug>-context.md` —
o mesmo lugar dos `-cc`/`-handoff`, para a `/archive-todos` recuperar; (4)
reporte o que estava AUSENTE (o gap de observabilidade fechado). Nunca siga um trabalho relevante sem
o archive existir.
