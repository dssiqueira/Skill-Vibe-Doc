---
version: alpha
name: Embarque
description: Painel interno de operação, sóbrio e denso, em que a cor só aparece para dizer o estado de cada etapa.
colors:
  primary: "#0E5A6E"
  primary-hover: "#0B4A5B"
  on-primary: "#FFFFFF"
  primary-soft: "#E3F1F4"
  surface: "#FFFFFF"
  background: "#F7F8FA"
  on-surface: "#172026"
  muted: "#5B6670"
  border: "#D5DADF"
  disabled: "#D5DADF"
  on-disabled: "#3F4A54"
  neutral-soft: "#EEF0F3"
  on-neutral-soft: "#3F4A54"
  info-soft: "#E0EAFB"
  on-info-soft: "#1E4FA8"
  success-soft: "#DCFCE7"
  on-success-soft: "#166534"
  warning-soft: "#FEF3C7"
  on-warning-soft: "#92400E"
  error: "#B42318"
  error-hover: "#8F1B12"
  error-soft: "#FEE4E2"
  on-error-soft: "#B42318"
typography:
  display:
    fontFamily: IBM Plex Sans
    fontSize: 24px
    fontWeight: 600
    lineHeight: 1.25
  title:
    fontFamily: IBM Plex Sans
    fontSize: 18px
    fontWeight: 600
    lineHeight: 1.3
  body-md:
    fontFamily: IBM Plex Sans
    fontSize: 14px
    fontWeight: 400
    lineHeight: 1.5
  body-sm:
    fontFamily: IBM Plex Sans
    fontSize: 13px
    fontWeight: 400
    lineHeight: 1.45
  label-md:
    fontFamily: IBM Plex Sans
    fontSize: 13px
    fontWeight: 600
    lineHeight: 1.2
  mono-sm:
    fontFamily: IBM Plex Mono
    fontSize: 12px
    fontWeight: 400
    lineHeight: 1.5
rounded:
  sm: 4px
  md: 6px
  full: 999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
components:
  page:
    backgroundColor: "{colors.background}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    padding: 24px
  page-title:
    textColor: "{colors.on-surface}"
    typography: "{typography.display}"
  section-title:
    textColor: "{colors.on-surface}"
    typography: "{typography.title}"
  nav-item-active:
    backgroundColor: "{colors.primary-soft}"
    textColor: "{colors.primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.sm}"
    padding: 8px
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 40px
  button-primary-hover:
    backgroundColor: "{colors.primary-hover}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 40px
  button-primary-disabled:
    backgroundColor: "{colors.disabled}"
    textColor: "{colors.on-disabled}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 40px
  button-secondary:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 40px
  button-danger:
    backgroundColor: "{colors.error}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 40px
  button-danger-hover:
    backgroundColor: "{colors.error-hover}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 40px
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 8px
    height: 40px
  input-error:
    backgroundColor: "{colors.error-soft}"
    textColor: "{colors.on-error-soft}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 8px
    height: 40px
  card-onboarding:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 16px
  card-onboarding-error:
    backgroundColor: "{colors.error-soft}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 16px
  divider:
    backgroundColor: "{colors.border}"
    height: 1px
  caption:
    textColor: "{colors.muted}"
    typography: "{typography.body-sm}"
  badge-pendente:
    backgroundColor: "{colors.neutral-soft}"
    textColor: "{colors.on-neutral-soft}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: 4px
  badge-em-andamento:
    backgroundColor: "{colors.info-soft}"
    textColor: "{colors.on-info-soft}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: 4px
  badge-aguardando-humano:
    backgroundColor: "{colors.warning-soft}"
    textColor: "{colors.on-warning-soft}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: 4px
  badge-concluida:
    backgroundColor: "{colors.success-soft}"
    textColor: "{colors.on-success-soft}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: 4px
  badge-erro:
    backgroundColor: "{colors.error-soft}"
    textColor: "{colors.on-error-soft}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: 4px
  timeline-step:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    padding: 12px
  timeline-step-manual:
    backgroundColor: "{colors.warning-soft}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 12px
  banner-error:
    backgroundColor: "{colors.error-soft}"
    textColor: "{colors.on-error-soft}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
  log-row:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.mono-sm}"
    padding: 8px
---

## Overview

Embarque é a ferramenta em que o backoffice passa o dia de olho na esteira de onboarding de clientes B2B. Três adjetivos: **sóbria, legível, honesta**. A tela deve passar a sensação de uma torre de controle calma: o que está andando fica quieto, o que travou salta aos olhos e já vem com o botão para destravar. Não é produto de vitrine; nenhum cliente final vê essa interface.

## Colors

- `primary` (petróleo) é a cor da ação: "Iniciar onboarding", "Tentar novamente", "Marcar como feito". Aparece em no máximo um botão por tela ou por bloco de etapa; o resto é `button-secondary`.
- `background` é o fundo da página; `surface` é o fundo de cards, tabelas e formulários. A diferença entre os dois substitui sombra.
- Cor de estado só aparece em badge, no marcador da linha do tempo e no card com erro. Cada estado tem um par fundo suave e texto escuro, todos com contraste acima de 5:1:
  - `neutral-soft`: pendente.
  - `info-soft`: em andamento (a automação está trabalhando).
  - `warning-soft`: aguardando humano (etapa manual ou aguardando assinatura do cliente).
  - `success-soft`: concluída.
  - `error-soft`: erro. É o único estado que muda o fundo do card inteiro no painel.
- `error` sólido só em `button-danger` (cancelar onboarding) e na borda esquerda do card com erro.
- `muted` para timestamps, CNPJ e textos de apoio. Nunca para informação que decide uma ação.

## Typography

Uma família: IBM Plex Sans para a interface e IBM Plex Mono só para log de auditoria, CNPJ e IDs, onde alinhamento de caractere ajuda a conferir.

- `display` (24px): título da página, um por tela.
- `title` (18px): nome do cliente no detalhe e títulos de seção.
- `body-md` (14px): texto padrão. Densidade de escritório, a Fernanda lê o dia todo em monitor.
- `body-sm` (13px): timestamps e legendas. Tamanho mínimo de texto da interface.
- `label-md` (13px, 600): botões, badges, cabeçalho de tabela.
- `mono-sm` (12px): linhas do log de auditoria. Única exceção abaixo de 13px, porque é texto de consulta, não de leitura corrida.

## Layout

- Desktop primeiro, alvo 1280px a 1920px. Navegação lateral fixa de 220px e conteúdo com largura máxima de 1200px.
- Painel em colunas por status (kanban de leitura), cada coluna com 280px mínimos; acima de 1440px as colunas se expandem.
- Detalhe do onboarding em duas colunas: linha do tempo das etapas (2/3) e dados do cliente (1/3). Log de auditoria em largura total abaixo.
- Espaçamento: `md` (16px) entre cards, `lg` (24px) entre seções, `xl` (32px) de respiro no topo da página.
- Abaixo de 768px (o Bruno no celular): navegação vira barra superior, colunas viram lista única ordenada por status, detalhe vira coluna única com a linha do tempo primeiro. Formulários de criação não precisam funcionar bem no celular.

## Elevation & Depth

Sem sombra no uso normal. Camadas são feitas por fundo (`background` sob `surface`) e borda de 1px em `border`. A única sombra permitida é a de modal (confirmação de cancelamento), para separar do conteúdo que ficou atrás. Card com erro ganha borda esquerda de 4px em `error`, não sombra.

## Shapes

- Cantos `md` (6px) em cards, botões e campos; `sm` (4px) em itens de navegação; `full` em badges.
- Ícones de traço (Lucide), 16px na interface e 20px no marcador da linha do tempo. Um ícone por estado: círculo vazio (pendente), círculo girando (em andamento), mão (aguardando humano), check (concluída), triângulo de alerta (erro).
- Sem ilustração. Estado vazio usa texto e um botão.

## Components

- **button-primary**: padrão em `primary`; hover em `button-primary-hover`; foco com contorno de 2px em `primary` afastado 2px; desabilitado em `button-primary-disabled` enquanto o formulário está inválido ou a ação já foi disparada (evita duplo clique que criaria dois envios de contrato).
- **button-secondary**: fundo `surface`, texto e borda em `primary`. Ações de apoio: "Ver log", "Copiar dados do cliente".
- **button-danger** e **button-danger-hover**: só para "Cancelar onboarding", sempre dentro de modal de confirmação com motivo obrigatório.
- **input** e **input-error**: campo com borda `border`; com erro, fundo `error-soft` e mensagem abaixo em `on-error-soft` dizendo o que corrigir ("CNPJ com dígito verificador inválido"). Foco com contorno em `primary`.
- **card-onboarding**: nome da empresa (`label-md`), plano, comercial responsável, etapa atual com badge e tempo desde o início em `caption`. **card-onboarding-error**: mesmo conteúdo, fundo `error-soft`, borda esquerda `error` e a mensagem de erro resumida em uma linha.
- **badge-pendente, badge-em-andamento, badge-aguardando-humano, badge-concluida, badge-erro**: texto sempre presente ao lado da cor ("Erro", "Aguardando você"), nunca só a cor.
- **timeline-step**: marcador com ícone de estado, nome da etapa, quem executa (Automático ou nome da pessoa) e timestamp em `caption`. Etapa com erro mostra `banner-error` com a mensagem e o botão "Tentar novamente". **timeline-step-manual**: fundo `warning-soft`, checklist da etapa manual e botão "Marcar como feito".
- **nav-item-active**: item da navegação lateral da tela atual.
- **page**, **page-title**, **section-title**, **divider**, **caption**: estrutura base de toda tela.
- **log-row**: uma linha por evento de auditoria, em `mono-sm`: data e hora, executado por, ação, detalhe. Linhas alternadas não mudam de cor; o `divider` separa.

## Do's and Don'ts

- Do: mostrar sempre quem executou cada etapa, "Automático" ou o nome da pessoa.
- Do: colocar a ação de destravar dentro do próprio bloco do erro, sem mandar a pessoa para outra tela.
- Do: escrever a mensagem de erro em português de gente ("O Sistema 2 recusou: e-mail já cadastrado"), com o código técnico só no log.
- Don't: usar cor de estado como decoração ou em botão.
- Don't: usar vermelho para "aguardando assinatura do cliente". Esperar o cliente não é erro.
- Don't: esconder etapa automática concluída; a linha do tempo mostra todas, do começo ao fim.
- Don't: animar nada além do ícone de "em andamento".
