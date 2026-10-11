---
version: alpha
name: Balcão TI
description: Ferramenta interna sóbria e densa, azul corporativo sobre cinza claro, com cor reservada para status e urgência.
colors:
  primary: "#1F4E8C"
  primary-hover: "#173D6E"
  on-primary: "#FFFFFF"
  background: "#F4F6F9"
  surface: "#FFFFFF"
  on-surface: "#1C2430"
  muted: "#5B6472"
  border: "#D5DAE1"
  sidebar: "#16202E"
  sidebar-active: "#24344A"
  on-sidebar: "#E6EAF0"
  critical: "#B42318"
  on-critical: "#FFFFFF"
  critical-soft: "#FDECEA"
  internal-note: "#FFF6DB"
  status-open-bg: "#DCE8F7"
  status-open-text: "#1F4E8C"
  status-progress-bg: "#FCEFC7"
  status-progress-text: "#6B4E00"
  status-waiting-bg: "#EDE7F6"
  status-waiting-text: "#4A2E83"
  status-resolved-bg: "#DDF1E4"
  status-resolved-text: "#1E6B3A"
  status-canceled-bg: "#ECEEF1"
  status-canceled-text: "#4A5260"
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
    fontSize: 15px
    fontWeight: 400
    lineHeight: 1.5
  body-sm:
    fontFamily: IBM Plex Sans
    fontSize: 13px
    fontWeight: 400
    lineHeight: 1.45
  label-md:
    fontFamily: IBM Plex Sans
    fontSize: 14px
    fontWeight: 600
    lineHeight: 1.2
  label-sm:
    fontFamily: IBM Plex Sans
    fontSize: 12px
    fontWeight: 600
    lineHeight: 1.2
    letterSpacing: 0.02em
  mono-sm:
    fontFamily: IBM Plex Mono
    fontSize: 13px
    fontWeight: 500
    lineHeight: 1.2
rounded:
  sm: 4px
  md: 6px
  lg: 8px
  full: 999px
spacing:
  xs: 4px
  sm: 8px
  md: 12px
  lg: 16px
  xl: 24px
  xxl: 40px
components:
  page:
    backgroundColor: "{colors.background}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    padding: "{spacing.xl}"
  page-title:
    textColor: "{colors.on-surface}"
    typography: "{typography.display}"
  section-title:
    textColor: "{colors.on-surface}"
    typography: "{typography.title}"
  sidebar:
    backgroundColor: "{colors.sidebar}"
    textColor: "{colors.on-sidebar}"
    typography: "{typography.label-md}"
    width: 220px
    padding: "{spacing.md}"
  sidebar-item-active:
    backgroundColor: "{colors.sidebar-active}"
    textColor: "{colors.on-sidebar}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 40px
    padding: "{spacing.sm}"
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 40px
    padding: "{spacing.lg}"
  button-primary-hover:
    backgroundColor: "{colors.primary-hover}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 40px
    padding: "{spacing.lg}"
  button-secondary:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 40px
    padding: "{spacing.lg}"
  button-danger:
    backgroundColor: "{colors.critical}"
    textColor: "{colors.on-critical}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 40px
    padding: "{spacing.lg}"
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.sm}"
    height: 40px
    padding: "{spacing.md}"
  field-error:
    textColor: "{colors.critical}"
    typography: "{typography.body-sm}"
  card:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.lg}"
    padding: "{spacing.lg}"
  ticket-row:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-sm}"
    height: 44px
    padding: "{spacing.md}"
  ticket-row-critical:
    backgroundColor: "{colors.critical-soft}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-sm}"
    height: 44px
    padding: "{spacing.md}"
  ticket-number:
    textColor: "{colors.muted}"
    typography: "{typography.mono-sm}"
  comment-public:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.lg}"
    padding: "{spacing.lg}"
  comment-internal:
    backgroundColor: "{colors.internal-note}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.lg}"
    padding: "{spacing.lg}"
  banner-attention:
    backgroundColor: "{colors.status-waiting-bg}"
    textColor: "{colors.status-waiting-text}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: "{spacing.md}"
  badge-status-open:
    backgroundColor: "{colors.status-open-bg}"
    textColor: "{colors.status-open-text}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: "{spacing.xs}"
  badge-status-progress:
    backgroundColor: "{colors.status-progress-bg}"
    textColor: "{colors.status-progress-text}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: "{spacing.xs}"
  badge-status-waiting:
    backgroundColor: "{colors.status-waiting-bg}"
    textColor: "{colors.status-waiting-text}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: "{spacing.xs}"
  badge-status-resolved:
    backgroundColor: "{colors.status-resolved-bg}"
    textColor: "{colors.status-resolved-text}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: "{spacing.xs}"
  badge-status-canceled:
    backgroundColor: "{colors.status-canceled-bg}"
    textColor: "{colors.status-canceled-text}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: "{spacing.xs}"
  badge-priority-critical:
    backgroundColor: "{colors.critical}"
    textColor: "{colors.on-critical}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.sm}"
    padding: "{spacing.xs}"
  caption:
    textColor: "{colors.muted}"
    typography: "{typography.body-sm}"
  divider:
    backgroundColor: "{colors.border}"
    height: 1px
  empty-state:
    textColor: "{colors.muted}"
    typography: "{typography.body-md}"
    padding: "{spacing.xxl}"
---

## Overview

O Balcão TI é uma ferramenta de trabalho, não uma vitrine. Atende dois públicos no mesmo visual: Marcos, que entra duas vezes por mês e precisa entender tudo sem ajuda, e Rafael, que passa 10 horas por dia na fila e precisa de densidade. Três adjetivos: confiável, calmo, legível. A sensação é a de um sistema corporativo bem cuidado, que some da frente e deixa o chamado aparecer.

## Colors

- `primary` (azul corporativo) é a cor da ação principal e do link. Aparece em um botão principal por tela: "Novo chamado" em Meus chamados, "Abrir chamado" no formulário, "Enviar" no detalhe. O resto é `button-secondary`.
- `background` é o fundo da aplicação; `surface` é o fundo de cartões, tabelas, formulários e comentários. O contraste entre os dois separa as áreas sem precisar de sombra.
- `on-surface` é o texto principal; `muted` é o texto de apoio (datas, "atualizado há", número do chamado, legendas). Nunca use `muted` para informação que a pessoa precisa para agir.
- `sidebar`, `sidebar-active` e `on-sidebar` só existem na barra lateral.
- Os pares `status-*` existem só para os selos de status, um por status: aberto (azul), em andamento (âmbar), aguardando solicitante (lilás), resolvido (verde), cancelado (cinza). O mesmo par lilás marca a faixa "O TI precisa de uma resposta sua", para ligar a faixa ao status.
- `critical` é reservado para prioridade crítica, ação destrutiva e erro. `critical-soft` pinta a linha inteira do chamado crítico na Fila. Se o vermelho aparecer em outra coisa, ele perde o sentido de urgência.
- `internal-note` (amarelo claro) é o fundo do comentário interno e de nada mais.
- Todos os pares de fundo e texto passam de 4,5:1.

## Typography

- Uma família, IBM Plex Sans, com IBM Plex Mono só para o número do chamado (`#1042`), que precisa ser lido e ditado por telefone sem confusão.
- `display` (24px) para o título da página. `title` (18px) para título de seção e título do chamado no detalhe.
- `body-md` (15px) para formulário, descrição e comentários: é o texto que o Marcos lê.
- `body-sm` (13px) para linhas da Fila e da tabela de usuários, onde a densidade importa, e para legendas e mensagens de erro de campo.
- `label-md` (14px, peso 600) para botões e itens da barra lateral; `label-sm` (12px, peso 600) só para selos.
- Tamanho mínimo: 12px, e só em selo. Texto corrido nunca abaixo de 13px.

## Layout

- Desktop primeiro, alvo de 1280px a 1920px. Barra lateral fixa de 220px à esquerda; conteúdo ocupa o resto com margem de 24px.
- Telas do solicitante (Meus chamados, Novo chamado, detalhe) têm largura máxima de 760px, centralizadas: pouco conteúdo, leitura confortável.
- Fila e Usuários usam a largura toda, em tabela. Linhas de 44px.
- Detalhe do analista: duas colunas, conteúdo e linha do tempo à esquerda (flexível), painel de ação à direita (320px, fixo ao rolar).
- Escala de espaçamento: 4, 8, 12, 16, 24, 40. Entre campos do formulário, 16px. Entre blocos da página, 24px. Dentro de cartões, 16px.
- Abaixo de 1024px a barra lateral vira só ícones; abaixo de 768px vira barra superior com menu e o painel de ação desce para baixo do título. Não precisa ser bonito no celular, precisa funcionar.

## Elevation & Depth

- Quase plano. A separação vem de fundo (`background` contra `surface`) e de borda de 1px em `border`.
- Cartões, tabela e comentários: borda de 1px, sem sombra.
- Sombra só em camada que flutua: menu de seletor, modal de confirmação e aviso temporário ("Salvo"). Uma sombra só, suave (0 4px 12px com 12% de opacidade).
- Modal de confirmação escurece o fundo com preto a 40%.

## Shapes

- Cantos de 6px em botão e item ativo da barra, 4px em campo e selo de prioridade, 8px em cartão e comentário. Selo de status em pílula.
- Ícones de linha, 20px, traço de 1,5px (conjunto Lucide). Ícone sempre acompanhado de rótulo na barra lateral e em botão; ícone sozinho só em ação de linha da tabela, com dica ao passar o mouse.
- Sem ilustração. Estado vazio é texto e, quando houver, um botão.

## Components

- **button-primary:** padrão em `primary`; hover em `button-primary-hover`; foco com anel de 2px em `primary` afastado 2px; desabilitado com 40% de opacidade e cursor bloqueado; carregando troca o rótulo por indicador e mantém a largura.
- **button-secondary:** fundo `surface`, texto `primary`, borda de 1px em `border`; hover com fundo `background`.
- **button-danger:** só dentro do modal de confirmação ("Cancelar chamado", "Desativar"). Nunca direto na tela.
- **input:** borda de 1px em `border`; foco com borda e anel em `primary`; erro com borda em `critical` e `field-error` logo abaixo; desabilitado com fundo `background`. Rótulo sempre visível acima do campo, nunca só placeholder.
- **sidebar e sidebar-item-active:** item ativo com fundo `sidebar-active` e barra de 3px em `on-sidebar` à esquerda; hover com o mesmo fundo a 60%.
- **page, page-title e section-title:** moldura de toda tela, título da página e títulos de seção.
- **card:** agrupa blocos no detalhe e no formulário.
- **ticket-row:** linha da Fila e de Meus chamados; hover com fundo `background`; linha selecionada por teclado com barra de 3px em `primary` à esquerda.
- **ticket-row-critical:** linha de chamado crítico, sempre com `badge-priority-critical` na coluna de prioridade.
- **ticket-number:** número do chamado em fonte mono.
- **badge-status-*:** um por status, texto sempre escrito ("Em andamento"), nunca só a cor.
- **badge-priority-critical:** só para prioridade crítica. Alta, média e baixa aparecem como texto `body-sm`, sem selo.
- **comment-public e comment-internal:** comentário interno tem fundo `internal-note` e rótulo "Interno" em `label-sm` no topo; o público fica em `surface`.
- **banner-attention:** faixa "O TI precisa de uma resposta sua" no detalhe do solicitante.
- **caption, divider e empty-state:** texto de apoio, separador de 1px e mensagem de estado vazio centralizada.

## Do's and Don'ts

- Do: um único botão `primary` por tela.
- Do: escrever o status por extenso no selo; a cor reforça, não substitui.
- Do: usar a mesma ordem de colunas em toda tabela de chamados.
- Do: mostrar "Salvo" por 2 segundos depois de mudança no painel do analista, em vez de modal.
- Don't: usar vermelho fora de crítico, erro e ação destrutiva.
- Don't: usar amarelo `internal-note` em qualquer coisa que o solicitante veja.
- Don't: aumentar o espaçamento da Fila para "respirar"; Rafael precisa ver 15 linhas sem rolar.
- Don't: usar ilustração, gradiente ou animação decorativa.
