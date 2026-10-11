---
version: alpha
name: Página Pronta
description: Interface neutra de papel e grafite, com um laranja queimado só para a ação principal, para que a página gerada com a marca do usuário seja sempre a estrela.
colors:
  primary: "#C2410C"
  primary-hover: "#9A3412"
  on-primary: "#FFFFFF"
  surface: "#FFFFFF"
  on-surface: "#1C1917"
  canvas: "#F5F5F4"
  muted: "#57534E"
  border: "#D6D3D1"
  selected: "#FFF7ED"
  disabled: "#E7E5E4"
  on-disabled: "#57534E"
  success-surface: "#DCFCE7"
  on-success-surface: "#166534"
  warning-surface: "#FEF3C7"
  on-warning-surface: "#92400E"
  error: "#B91C1C"
  error-surface: "#FEE2E2"
  on-error-surface: "#991B1B"
  inverse: "#1C1917"
  on-inverse: "#FAFAF9"
typography:
  display:
    fontFamily: Manrope
    fontSize: 32px
    fontWeight: 700
    lineHeight: 1.15
    letterSpacing: -0.02em
  question:
    fontFamily: Manrope
    fontSize: 24px
    fontWeight: 600
    lineHeight: 1.25
  title:
    fontFamily: Manrope
    fontSize: 18px
    fontWeight: 600
    lineHeight: 1.3
  body-md:
    fontFamily: Manrope
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
  body-sm:
    fontFamily: Manrope
    fontSize: 14px
    fontWeight: 400
    lineHeight: 1.45
  label-md:
    fontFamily: Manrope
    fontSize: 14px
    fontWeight: 600
    lineHeight: 1.2
  label-sm:
    fontFamily: Manrope
    fontSize: 12px
    fontWeight: 600
    lineHeight: 1.2
rounded:
  sm: 4px
  md: 8px
  lg: 12px
  full: 999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 40px
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 14px
    height: 48px
  button-primary-hover:
    backgroundColor: "{colors.primary-hover}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 14px
    height: 48px
  button-primary-disabled:
    backgroundColor: "{colors.disabled}"
    textColor: "{colors.on-disabled}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 14px
    height: 48px
  button-secondary:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 14px
    height: 48px
  briefing-question:
    backgroundColor: "{colors.canvas}"
    textColor: "{colors.on-surface}"
    typography: "{typography.question}"
    padding: 24px
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 48px
  input-error:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.error}"
    typography: "{typography.body-sm}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 48px
  option-card:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.title}"
    rounded: "{rounded.lg}"
    padding: 16px
  option-card-selected:
    backgroundColor: "{colors.selected}"
    textColor: "{colors.on-surface}"
    typography: "{typography.title}"
    rounded: "{rounded.lg}"
    padding: 16px
  step-indicator:
    backgroundColor: "{colors.primary}"
    rounded: "{rounded.full}"
    height: 4px
  step-indicator-track:
    backgroundColor: "{colors.border}"
    rounded: "{rounded.full}"
    height: 4px
  editor-panel:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    padding: 16px
  preview-frame:
    backgroundColor: "{colors.canvas}"
    rounded: "{rounded.lg}"
    padding: 24px
  list-item:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.lg}"
    padding: 16px
  page-title:
    textColor: "{colors.on-surface}"
    typography: "{typography.display}"
  caption:
    textColor: "{colors.muted}"
    typography: "{typography.body-sm}"
  divider:
    backgroundColor: "{colors.border}"
    height: 1px
  badge-success:
    backgroundColor: "{colors.success-surface}"
    textColor: "{colors.on-success-surface}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 4px
  badge-warning:
    backgroundColor: "{colors.warning-surface}"
    textColor: "{colors.on-warning-surface}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 4px
  alert-error:
    backgroundColor: "{colors.error-surface}"
    textColor: "{colors.on-error-surface}"
    typography: "{typography.body-sm}"
    rounded: "{rounded.md}"
    padding: 12px
  banner-offline:
    backgroundColor: "{colors.inverse}"
    textColor: "{colors.on-inverse}"
    typography: "{typography.body-sm}"
    padding: 12px
---

## Overview

Página Pronta é ferramenta, não vitrine. Quem usa é o founder técnico que quer a LP numa noite e a profissional autônoma que nunca abriu um editor de site. A interface precisa passar três sensações: **calma, rápida e confiável**. Ela recua para que a página gerada, com as cores e a fonte da marca do usuário, apareça como o que importa na tela.

Este arquivo descreve só a interface do produto. A página que o produto gera segue o DESIGN.md da marca do usuário, nunca este.

## Colors

- `primary` (laranja queimado): só a ação principal da tela, no máximo uma vez por tela: "Criar minha página", "Continuar", "Gerar minha página", "Exportar". Hover em `primary-hover`. Contraste do texto branco: 5,2:1.
- `surface` e `on-surface`: fundo e texto padrão de painéis, campos e cartões.
- `canvas`: fundo do app e moldura do preview. O cinza quente separa a interface da página gerada, que costuma ter fundo branco.
- `muted`: textos de apoio, contadores de caracteres, datas.
- `border`: bordas de campos e cartões, divisores e trilho da barra de passos.
- `selected`: fundo do cartão de opção escolhido (tom, CTA, marca), sempre junto com borda em `primary`.
- `disabled` e `on-disabled`: botões indisponíveis (sem conexão, sem crédito).
- `success-surface`, `warning-surface`, `error-surface` com seus `on-`: status e avisos. Amarelo marca "Preencha antes de publicar" e "Revise antes de publicar"; vermelho, erro de geração ou de marca.
- `inverse`: banner de sem conexão e toasts.
- Nunca use a cor da marca do usuário na interface do produto; ela só existe dentro do preview e das miniaturas de marca.

## Typography

- Uma família: Manrope, pelo Google Fonts, com fallback `system-ui, sans-serif`.
- `display`: título de tela (Home, Minhas páginas, Minhas marcas, Planos). Uma vez por tela.
- `question`: a pergunta atual do briefing. É o maior texto do fluxo de geração.
- `title`: nomes em cartões de opção e títulos de bloco no painel de edição.
- `body-md`: texto de campos e listas. `body-sm`: apoio, avisos e mensagens de erro.
- `label-md`: botões. `label-sm`: badges. Nada abaixo de 12px; no celular, campos sempre em 16px para o navegador não dar zoom.

## Layout

- Grid de 12 colunas, largura máxima de 1280px; o briefing é uma coluna central de até 640px.
- Preview e edição no notebook: painel de edição com 40% da largura (mínimo 360px) e preview com 60%. Abaixo de 1024px, vira abas "Ver página" e "Editar texto".
- Espaçamento: `md` (16px) entre campos, `lg` (24px) entre blocos, `xl` (40px) entre seções da Home.
- Margem lateral de 16px no celular; botão de ação principal com largura total e fixo no rodapé.
- Alvos de toque de pelo menos 48px.

## Elevation & Depth

- Interface quase plana: separação por cor (`canvas` contra `surface`) e borda de 1px em `border`.
- Uma sombra só, suave (0 1px 3px a 12% de opacidade), para modais, o preview e o botão fixo no rodapé do celular.
- Modal escurece o fundo com `inverse` a 40% de opacidade.

## Shapes

- `rounded.md` (8px) em botões, campos e alertas; `rounded.lg` (12px) em cartões, itens de lista e moldura do preview; `rounded.full` em badges e na barra de passos.
- Ícones de traço de 1,5px, 20px, da biblioteca Lucide. Sem ilustração: o exemplo visual do produto são as próprias páginas geradas.

## Components

- **button-primary:** padrão laranja; hover em `button-primary-hover`; foco com anel de 2px em `primary` afastado 2px; desabilitado em `button-primary-disabled`; carregando troca o texto por "Gerando..." e mantém a largura.
- **button-secondary:** fundo `surface` com borda `border`; usado em "Voltar", "Gerar novamente", "Arquivar". Hover escurece a borda para `muted`.
- **briefing-question:** bloco da pergunta atual no fundo `canvas`, com o campo logo abaixo.
- **input:** borda `border`, foco com borda e anel em `primary`; erro em `input-error`, com borda `error` e a mensagem abaixo em `body-sm`. Desabilitado usa `disabled`.
- **option-card:** cartões de tom, CTA, tema e marca; selecionado em `option-card-selected` com borda de 2px em `primary` e ícone de check. Foco igual ao do botão.
- **step-indicator:** barra de 6 passos do briefing; o trecho concluído em `step-indicator`, o restante em `step-indicator-track`.
- **editor-panel:** painel de textos; cada bloco separado por `divider`, com título em `title` e badge quando houver aviso.
- **preview-frame:** moldura do iframe e das miniaturas de página e de marca.
- **list-item:** item de Minhas páginas e Minhas marcas, com miniatura à esquerda, `caption` com data e marca, e badge de status.
- **page-title:** título de tela em `display`.
- **badge-success:** "Exportada". **badge-warning:** "Preencha antes de publicar", "Revise antes de publicar", "Marca atualizada".
- **alert-error:** erro de geração e erros do DESIGN.md importado, sempre com uma ação ("Tentar de novo", "Corrigir automaticamente").
- **banner-offline:** faixa no topo, fixa, enquanto não houver conexão.

## Do's and Don'ts

- Do: deixar a página gerada ocupar o maior espaço da tela; a interface é moldura.
- Do: usar `primary` uma vez por tela, só na ação que leva adiante.
- Do: escrever avisos em linguagem do dia a dia ("o texto ficaria difícil de ler", não "contraste insuficiente no token on-primary").
- Don't: aplicar a cor ou a fonte da marca do usuário fora do preview e das miniaturas.
- Don't: oferecer controles de cor, fonte ou espaçamento na tela de edição.
- Don't: usar barra de progresso com percentual na geração.
- Don't: criar cor, tamanho ou espaçamento fora deste arquivo; proponha e atualize aqui.
