# schematize-archive — sempre-on

O `<projeto>_archive/` é CRITICIDADE 0: guardar o histórico (checklists, planos, decisões/ADRs,
handoffs de chat, índice) NÃO é opcional. Archive ausente = bug de observabilidade — criá-lo é o 1º
item. Toda decisão/plano/handoff relevante vira arquivo durável no archive (o operacional vivo é
`.schematize/`; o espelho durável é o archive). Pra recuperar o que faltou e montar o próximo trabalho:
`/archive-todos` (gera afazeres pro overdev do histórico recuperável).
