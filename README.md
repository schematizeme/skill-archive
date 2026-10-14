# schematize-archive

> **O archive da casa como CRITICIDADE 0** — armazenar o histórico da evolução do sistema **não é
> opcional**. Rege o `<projeto>/<projeto>_archive/` obrigatório (checklists, planos, decisões/ADRs,
> handoffs de contexto/chat, índice/MAPA, relatórios de audit/pentest, snapshots do overdev): o
> rastro **durável e recuperável** que responde, a qualquer momento, *o que foi decidido,
> planejado, feito — e o que ficou aberto*. Archive ausente = **bug de observabilidade**.

Pacote de **skill normativa para [Claude Code](https://claude.com/claude-code)**.
Parte do catálogo **schematize skills**. Disciplina **agnóstica de linguagem** que pareia com a
`schematize-engineering` (a base: archive §28, overdev, índice §39), com a `schematize-audit` (o
oráculo dos órfãos RED) e com a `schematize-overdev-context` (a Fase 0, que consome o que esta
skill recupera).

## Instalar

### Pelo app schematize (recomendado)

```bash
schematize install archive    # requer o CLI schematize instalado
```

### Última versão (a partir de um clone)

```bash
git clone https://github.com/schematizeme/skill-archive.git
cd skill-archive && ./install.sh           # instala no projeto atual
# ./install.sh /caminho/do/projeto           # ou aponte para outro projeto
```

Ou baixe o `.zip` da última release e descompacte em `.claude/skills/`:

```bash
curl -L -o skill-archive.zip \
  https://github.com/schematizeme/skill-archive/releases/latest/download/skill-archive.zip
unzip skill-archive.zip -d .claude/skills/
```

## O que tem dentro

- **SKILL.md** — o contrato: o archive é obrigatório, é **repo git próprio e privado**, e o que
  mora dentro dele (`overdev/ index/ decisoes/ chats/ context/ context_agent/ plan/ scan/ qa/ audit/ pentest/ orchestration/ scaffold/`).
- **references/** — `archive` (a estrutura obrigatória e o ciclo de vida), `gerar-afazeres` (como
  transformar o histórico recuperável em checklist de overdev, com disciplina red-first).
- **scripts/** — `check-archive.sh` (o gate: segredo/PII/binário/convenção, com 17 casos de teste) e
  `collect-history.sh`: enumera **por contagem** todo o histórico recuperável
  (checklists nas 3 classes, handoffs em `chats/` **e** `context/`, ADRs `proposed`, perguntas
  parkeadas, premature-stops, TODO/FIXME) e **reprova** quando não há archive ou não há histórico.
  É o passo 1 do `/archive-todos` — sem ele a varredura vira memória.
- **assets/commands/** — `/archive-help`, `/archive-init` (materializa a estrutura e o repo),
  `/archive-check` (o gate do que nunca pode entrar), `/archive-todos` (gera os afazeres do overdev).
- **assets/CLAUDE.md** — regra sempre-on: archive é criticidade 0; decisão/plano/handoff vira
  arquivo durável.
- **gui.json** — os botões **Archive** (`/archive-init`) e **Afazeres** (`/archive-todos`) na GUI.

## Comandos

| Comando | O que faz |
|---|---|
| `/archive-help` | lista os comandos da skill |
| `/archive-init` | materializa o `<projeto>/<projeto>_archive/` (estrutura + **`git init` e remote privado**), espelha o `.schematize/`, grava o handoff da sessão e reporta o que estava ausente |
| `/archive-check` | o gate: varre o archive antes do commit — segredo, PII, binário, `.gitignore` interno, ADR duplicado, convenção de nome — e lembra o ensaio de recuperação |
| `/archive-todos` | gera os afazeres do overdev a partir do histórico recuperável (checklists nas 3 classes, ADRs `proposed`, perguntas parkeadas, premature-stops), com disciplina red-first |

## Versão

**v0.2.0** — changelog completo em `CHANGELOG.md`. Instalação e bump seguem o padrão do catálogo
(`VERSION`, `skill.toml`, frontmatter e linha do `SKILL.md`, mais o `skills.json` derivado).

## Regra de ouro

**Histórico que não está gravado não existe.** O operacional vivo é o `.schematize/`; o **espelho
durável é o archive** — e é dele que a auditoria, a retomada e o `/archive-todos` recuperam a
evolução. Uma varredura que devolve vazio **sem erro** é o pior modo de falha possível aqui: por
isso o `collect-history.sh` sai 1 quando não achou nada, em vez de deixar você concluir que a
história era curta.

## Relação com as outras skills

- **schematize-engineering** — a BASE que exige o archive (§28), o overdev (§0/§2) e o índice (§39).
- **schematize-audit** — o veredito: `/archive-todos` deriva o saneamento, `/audit-run` cobra
  cobertura A/A e trava em órfão RED.
- **schematize-overdev-context** — a Fase 0: consome o que esta skill recuperou (DECISOES, PLAN,
  CHECKLIST) e monta o briefing do overdev.

MIT.
