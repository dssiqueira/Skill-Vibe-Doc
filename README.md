# Vibe Doc

**O briefing que transforma prompt em produto, agora como skill.**

Um PRD é para um dev que faz perguntas. Um Vibe Doc é para uma IA que assume. Esta skill faz a IA assumir certo: entrevista você, escreve o Vibe Doc do seu produto e mantém tudo atualizado enquanto o código anda.

Criado por [Douglas Siqueira](https://doug.ia.br/vibedoc).

## Instalar

**Com o Skills CLI** (Claude Code, Codex, Cursor e outras ferramentas compatíveis com o padrão aberto de Agent Skills):

```bash
npx skills add dssiqueira/skill-vibe-doc
```

**No Claude Code, na mão:**

```bash
git clone https://github.com/dssiqueira/skill-vibe-doc
cp -r skill-vibe-doc/skills/vibe-doc ~/.claude/skills/
```

**No app do Claude:** compacte a pasta `skills/vibe-doc` em um .zip e envie na área de Skills das configurações.

## Usar

Abra o seu projeto e peça, do seu jeito:

- *"Cria o Vibe Doc desse projeto"*: a skill entrevista você em blocos curtos e gera tudo.
- *"Atualiza o Vibe Doc com o que mudei hoje"*: lê o que mudou e mexe só nos arquivos afetados.
- *"Revisa o Vibe Doc"*: aponta contradição, doc atrás do código e trecho vago, do mais grave ao menos.
- *"Migra meu Vibe Doc antigo"*: transforma o layout.md em fluxos.md mais DESIGN.md.

## O que ela gera

```
AGENTS.md              porta de entrada que qualquer agente lê primeiro
DESIGN.md              a cara do produto, no padrão aberto do Google
docs/
├── contexto.md        problema, escopo, o que não é, critério de sucesso e de morte
├── personas.md        quem usa, em que situação, o que evita
├── estruturadedados.md  entidades, campos e regras de negócio
├── fluxos.md          telas, fluxos e estados
├── metricas.md        o que medir e quais eventos registrar
├── integracoes.md     autenticação, banco, APIs, infraestrutura
└── decisoes.md        decisões técnicas com alternativa descartada e motivo
```

### O que mudou na versão 3

- **DESIGN.md no lugar da parte visual do layout.md.** O [DESIGN.md](https://github.com/google-labs-code/design.md) é o padrão aberto do Google Labs para identidade visual: tokens que a máquina aplica e regras que orientam o julgamento. Valide com `npx @google/design.md lint DESIGN.md` e exporte para Tailwind com `npx @google/design.md export --format css-tailwind DESIGN.md`.
- **fluxos.md** fica só com telas, fluxos e estados. Um assunto por arquivo.
- **AGENTS.md** como entrada única. No Claude Code, um `CLAUDE.md` com `@AGENTS.md` basta.
- **decisoes.md** registra cada decisão técnica, inclusive o nível de autonomia quando há IA no meio: entre duas soluções que resolvem a mesma dor, vence a mais simples.
- **Critério de sucesso e de morte** no contexto, definidos antes de construir.

## Exemplos

Cinco Vibe Docs completos em [`exemplos/`](exemplos), todos com DESIGN.md validado pelo lint oficial:

| Pasta | Produto |
|---|---|
| [`01-app-b2c-personal-trainer`](exemplos/01-app-b2c-personal-trainer) | App mobile para personal trainers |
| [`02-saas-b2b-interno`](exemplos/02-saas-b2b-interno) | Ferramenta interna de chamados de TI |
| [`03-marketplace`](exemplos/03-marketplace) | Marketplace de serviços locais |
| [`04-ferramenta-automacao`](exemplos/04-ferramenta-automacao) | Automação de onboarding de clientes |
| [`05-criacao-de-lps`](exemplos/05-criacao-de-lps) | Gerador de landing pages com IA |

## Sem agente?

Os esqueletos estão em [`skills/vibe-doc/templates`](skills/vibe-doc/templates). Copie para o seu projeto e preencha seguindo [`references/arquivos.md`](skills/vibe-doc/references/arquivos.md).

## Mais

- Página do método: [doug.ia.br/vibedoc](https://doug.ia.br/vibedoc)
- Handbook *Vibe Coding na Prática*: [doug.ia.br/handbooks/vibe-coding-pm-builder](https://doug.ia.br/handbooks/vibe-coding-pm-builder)

Licença MIT. Use, adapte e compartilhe.
