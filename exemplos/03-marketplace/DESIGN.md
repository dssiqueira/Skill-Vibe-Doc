---
version: alpha
name: Resolve Aí
description: "Verde-petróleo de confiança sobre fundo claro e quente, letra grande e legível, status com cor e texto. Feito para quem tem pressa e para quem tem pouca intimidade com app."
colors:
  primary: "#0F5C4D"
  primary-hover: "#0B4A3E"
  on-primary: "#FFFFFF"
  background: "#F6F5F1"
  on-background: "#1C2321"
  surface: "#FFFFFF"
  on-surface: "#1C2321"
  muted: "#5B6461"
  border: "#D3D7D3"
  disabled: "#E4E6E3"
  on-disabled: "#5B6461"
  rating: "#9A5800"
  error: "#B42318"
  on-error: "#FFFFFF"
  error-soft: "#FDE8E6"
  status-open: "#E3EDFB"
  on-status-open: "#1849A9"
  status-offers: "#FDEBD3"
  on-status-offers: "#8A3209"
  status-progress: "#DCF2E3"
  on-status-progress: "#14612A"
  status-done: "#ECEDEC"
  on-status-done: "#454B49"
typography:
  display:
    fontFamily: Atkinson Hyperlegible
    fontSize: 28px
    fontWeight: 700
    lineHeight: 1.2
    letterSpacing: -0.01em
  title:
    fontFamily: Atkinson Hyperlegible
    fontSize: 20px
    fontWeight: 700
    lineHeight: 1.3
  body-lg:
    fontFamily: Atkinson Hyperlegible
    fontSize: 18px
    fontWeight: 400
    lineHeight: 1.5
  body-md:
    fontFamily: Atkinson Hyperlegible
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
  label-md:
    fontFamily: Atkinson Hyperlegible
    fontSize: 16px
    fontWeight: 700
    lineHeight: 1.2
  label-sm:
    fontFamily: Atkinson Hyperlegible
    fontSize: 14px
    fontWeight: 700
    lineHeight: 1.2
rounded:
  sm: 6px
  md: 10px
  lg: 16px
  full: 999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 40px
components:
  page:
    backgroundColor: "{colors.background}"
    textColor: "{colors.on-background}"
    typography: "{typography.body-md}"
    padding: "{spacing.md}"
  page-title:
    textColor: "{colors.on-background}"
    typography: "{typography.display}"
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 14px
    height: 52px
  button-primary-hover:
    backgroundColor: "{colors.primary-hover}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 52px
  button-primary-disabled:
    backgroundColor: "{colors.disabled}"
    textColor: "{colors.on-disabled}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 52px
  button-secondary:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 14px
    height: 52px
  button-danger:
    backgroundColor: "{colors.error}"
    textColor: "{colors.on-error}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 52px
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-lg}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 52px
  input-error:
    backgroundColor: "{colors.error-soft}"
    textColor: "{colors.error}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    height: 52px
  chip-categoria:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.label-md}"
    rounded: "{rounded.lg}"
    padding: 12px
    height: 88px
  chip-categoria-selected:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.lg}"
    padding: 12px
    height: 88px
  card-pedido:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.lg}"
    padding: 16px
  card-proposta:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.lg}"
    padding: 16px
  card-title:
    textColor: "{colors.on-surface}"
    typography: "{typography.title}"
  rating:
    textColor: "{colors.rating}"
    typography: "{typography.label-md}"
  avatar:
    backgroundColor: "{colors.disabled}"
    rounded: "{rounded.full}"
    size: 56px
  badge-status-aberto:
    backgroundColor: "{colors.status-open}"
    textColor: "{colors.on-status-open}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  badge-status-com-propostas:
    backgroundColor: "{colors.status-offers}"
    textColor: "{colors.on-status-offers}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  badge-status-em-andamento:
    backgroundColor: "{colors.status-progress}"
    textColor: "{colors.on-status-progress}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  badge-status-concluido:
    backgroundColor: "{colors.status-done}"
    textColor: "{colors.on-status-done}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  badge-urgente:
    backgroundColor: "{colors.error-soft}"
    textColor: "{colors.error}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  toggle-disponivel-on:
    backgroundColor: "{colors.status-progress}"
    textColor: "{colors.on-status-progress}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    height: 48px
  toggle-disponivel-off:
    backgroundColor: "{colors.status-done}"
    textColor: "{colors.on-status-done}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    height: 48px
  caption:
    textColor: "{colors.muted}"
    typography: "{typography.label-sm}"
  divider:
    backgroundColor: "{colors.border}"
    height: 1px
  bottom-nav:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.muted}"
    typography: "{typography.label-sm}"
    height: 64px
  bottom-nav-active:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.primary}"
    typography: "{typography.label-sm}"
    height: 64px
  toast-error:
    backgroundColor: "{colors.on-surface}"
    textColor: "{colors.surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 16px
---

## Overview

Confiável, direto e acolhedor. O Resolve Aí atende dois públicos ao mesmo tempo: a Cláudia, que está com pressa e com medo de pôr um desconhecido dentro de casa, e o Seu João, eletricista de 48 anos que lê no celular com o braço esticado e desiste de app complicado. A tela tem que passar segurança para ela e parecer ferramenta de trabalho séria para ele: nada de enfeite, letra grande, uma ação clara por tela.

A identidade é uma proposta. Dá para trocar a cor primária e a fonte sem mexer em mais nada, desde que o contraste continue acima de 4,5:1.

## Colors

- `primary` (verde-petróleo): a cor da ação principal e de nada mais. Aparece no máximo uma vez por tela como botão cheio (`button-primary`): "Publicar pedido", "Enviar proposta", "Aceitar proposta". Nos cards e na navegação ela vira só cor de texto.
- `background` (off-white quente) é o fundo da página; `surface` (branco) é o fundo de card, campo e barra de navegação. A diferença entre os dois separa os blocos sem precisar de sombra.
- `muted`: texto secundário (bairro, "há 2 h", distância). Nunca para informação que decide a escolha.
- `rating`: âmbar escuro, só para estrelas e nota média. É a única cor quente fora dos status, para a reputação saltar em todo lugar onde um profissional aparece.
- Status do pedido sempre em par fundo claro mais texto escuro: aberto (`status-open`, azul), com propostas (`status-offers`, laranja), em andamento (`status-progress`, verde), concluído (`status-done`, cinza). Cancelado e expirado usam o par de concluído com outro texto.
- `error` e `error-soft`: erro de campo, selo "Urgente" e ação destrutiva (cancelar pedido). Urgência e erro dividem a cor de propósito: os dois pedem atenção imediata.

## Typography

Uma família só: Atkinson Hyperlegible, desenhada para baixa visão, com letras que não se confundem (I, l, 1; O, 0). Serve ao Seu João sem parecer app de acessibilidade.

- `display` (28px): título da tela. Um por tela.
- `title` (20px): título do pedido no card e nome do profissional.
- `body-lg` (18px): texto digitado em campos. Quem digita precisa ver o que digitou sem óculos.
- `body-md` (16px): texto corrido, descrição do pedido, mensagem da proposta.
- `label-md` (16px, negrito): botões, chips de categoria, nota média.
- `label-sm` (14px, negrito): selos de status, legenda, navegação inferior. É o menor tamanho permitido no produto.

## Layout

- Mobile-first em coluna única. Margem lateral de `md` (16px), espaço entre blocos de `lg` (24px), entre itens de uma lista de `sm` (8px).
- Largura máxima de conteúdo: 480px no celular e no desktop do morador (formulário e propostas não ganham nada esticando). A área do profissional no desktop usa até 960px, com a lista de pedidos em duas colunas de cards a partir de 768px.
- Botão principal fica fixo no rodapé da tela em formulários (Novo pedido, Enviar proposta), sempre visível acima do teclado.
- Navegação inferior com no máximo 3 itens, altura de 64px. No desktop ela vira barra lateral esquerda.
- Alvo de toque mínimo de 48px em tudo que é clicável.

## Elevation & Depth

Quase plano. Card é `surface` sobre `background` com borda de 1px em `border`, sem sombra. A única sombra do produto é a do botão fixo no rodapé e a do toast (sombra curta, 0 2px 8px com 12% de opacidade), para mostrar que estão por cima do conteúdo que rola. Modal escurece o fundo com preto a 40%.

## Shapes

- Cantos: `md` (10px) em botão e campo, `lg` (16px) em card e chip de categoria, `full` em selo, toggle e foto de perfil.
- Ícones de traço, 24px, espessura 2px, uma cor só (a do texto ao lado). Cada categoria tem um ícone fixo: raio (Elétrica), gota (Hidráulica), balde (Limpeza), rolo (Pintura), chave inglesa (Pequenos reparos).
- Foto do profissional sempre redonda (`avatar`, 56px na lista, 96px no perfil). Sem foto, mostra as iniciais sobre `disabled`.
- Sem ilustração decorativa. Estado vazio usa o ícone da categoria grande e uma frase.

## Components

- **button-primary**: padrão em `primary`; hover e pressionado em `button-primary-hover`; foco com anel de 3px em `primary` afastado 2px; desabilitado em `button-primary-disabled`, com o motivo escrito logo acima ("Escolha uma categoria"); carregando troca o texto por "Enviando..." e bloqueia novo toque.
- **button-secondary**: fundo `surface`, borda e texto em `primary`. Para "Ver perfil completo", "Chamar no WhatsApp" e ações que não fecham o fluxo.
- **button-danger**: só para confirmar cancelamento de pedido ou proposta, dentro de modal. Nunca na tela principal.
- **input**: borda de 1px em `border`, rótulo acima em `label-sm`, nunca só placeholder. Foco troca a borda para `primary` com 2px. Erro usa `input-error` e mostra a mensagem embaixo em `error`, dizendo o que fazer ("Digite um CEP com 8 números").
- **chip-categoria**: bloco de 88px de altura com ícone e nome, em grade de 2 colunas. Selecionado vira `chip-categoria-selected`. Toque troca a seleção, não acumula.
- **card-pedido**: título em `card-title`, selo de status ou de urgência no canto superior direito, linha de `caption` com categoria, bairro, distância e tempo desde a abertura. Toque no card inteiro abre o detalhe.
- **card-proposta**: `avatar`, nome em `card-title`, `rating` com estrelas e número de avaliações ("4,8 · 23 avaliações"), valor em `title`, prazo e mensagem cortada em 3 linhas. Profissional sem avaliação mostra "Novo no Resolve Aí" em `caption` no lugar das estrelas.
- **rating**: estrelas cheias em `rating`, vazias em `border`, sempre com o número ao lado (estrela sozinha não é lida por leitor de tela).
- **badge-status-***: texto sempre presente além da cor ("Aberto", "3 propostas", "Em andamento", "Concluído").
- **badge-urgente**: "Urgente" com ícone de relógio. Aparece no card do profissional e no detalhe do pedido.
- **toggle-disponivel-on / -off**: barra larga no topo da tela inicial do profissional, texto "Disponível para pedidos" ou "Indisponível". Mudança tem efeito na hora e mostra confirmação em `caption`.
- **bottom-nav / bottom-nav-active**: item ativo em `primary` com ícone preenchido; inativos em `muted` com ícone de traço.
- **toast-error**: fundo escuro, texto claro, some em 5 segundos, com ação "Tentar de novo" quando faz sentido.
- **page / page-title / caption / divider**: base de toda tela, título único, texto secundário e separador entre seções do perfil.

## Do's and Don'ts

- Do: mostrar nota e número de avaliações em todo lugar onde um profissional aparece.
- Do: escrever o status por extenso no selo; cor sozinha não informa.
- Do: manter um único `button-primary` por tela.
- Do: usar números grandes e formatados em reais ("R$ 180") no valor da proposta.
- Don't: usar `primary` como fundo de card ou de seção.
- Don't: usar texto menor que 14px, nem cinza mais claro que `muted`.
- Don't: esconder ação importante atrás de menu de três pontinhos; o Seu João não vai achar.
- Don't: usar verde de marca de terceiros (WhatsApp) no botão de contato; o ícone basta.
