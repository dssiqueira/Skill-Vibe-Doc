---
version: alpha
name: Treinou
description: Ferramenta de trabalho para usar em pé, com uma mão e na luz da academia. Fundo claro, verde só para a ação, horário em destaque.
colors:
  primary: "#0B7A3E"
  on-primary: "#FFFFFF"
  primary-pressed: "#0A6B37"
  primary-soft: "#E3F3E8"
  on-primary-soft: "#0A6B37"
  background: "#F3F4EF"
  on-background: "#14181F"
  surface: "#FFFFFF"
  on-surface: "#14181F"
  muted: "#5A6270"
  border: "#D9DCD3"
  surface-disabled: "#E8EAE4"
  warning-soft: "#FBEBDD"
  on-warning-soft: "#8F4400"
  error: "#B42318"
  on-error: "#FFFFFF"
  error-soft: "#FDE8E6"
  inverse: "#14181F"
  on-inverse: "#FFFFFF"
  accent-on-inverse: "#86E0A8"
typography:
  display:
    fontFamily: Barlow Semi Condensed
    fontSize: 28px
    fontWeight: 700
    lineHeight: 1.15
    letterSpacing: -0.01em
  time:
    fontFamily: Barlow Semi Condensed
    fontSize: 26px
    fontWeight: 600
    lineHeight: 1
  title:
    fontFamily: Inter
    fontSize: 20px
    fontWeight: 600
    lineHeight: 1.3
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
  body-strong:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: 600
    lineHeight: 1.4
  label-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: 600
    lineHeight: 1.2
  label-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: 600
    lineHeight: 1.2
  caption:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: 400
    lineHeight: 1.4
rounded:
  sm: 6px
  md: 12px
  lg: 20px
  full: 999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
components:
  screen:
    backgroundColor: "{colors.background}"
    textColor: "{colors.on-background}"
  screen-title:
    textColor: "{colors.on-background}"
    typography: "{typography.display}"
  section-title:
    textColor: "{colors.on-background}"
    typography: "{typography.title}"
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 16px
    height: 52px
  button-primary-pressed:
    backgroundColor: "{colors.primary-pressed}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 16px
    height: 52px
  button-primary-disabled:
    backgroundColor: "{colors.surface-disabled}"
    textColor: "{colors.muted}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 16px
    height: 52px
  button-secondary:
    backgroundColor: "{colors.primary-soft}"
    textColor: "{colors.on-primary-soft}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 16px
    height: 52px
  button-destructive:
    backgroundColor: "{colors.error}"
    textColor: "{colors.on-error}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 16px
    height: 52px
  button-presente:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    height: 48px
    width: 112px
  link:
    textColor: "{colors.primary}"
    typography: "{typography.label-md}"
  card-agenda:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-strong}"
    rounded: "{rounded.md}"
    padding: 16px
  card-agenda-registrado:
    backgroundColor: "{colors.background}"
    textColor: "{colors.muted}"
    typography: "{typography.body-strong}"
    rounded: "{rounded.md}"
    padding: 16px
  card-agenda-time:
    textColor: "{colors.on-surface}"
    typography: "{typography.time}"
  list-item-aluno:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-strong}"
    padding: 16px
    height: 72px
  avatar:
    backgroundColor: "{colors.primary-soft}"
    textColor: "{colors.on-primary-soft}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    size: 48px
  avatar-lg:
    backgroundColor: "{colors.primary-soft}"
    textColor: "{colors.on-primary-soft}"
    typography: "{typography.display}"
    rounded: "{rounded.full}"
    size: 88px
  badge-presente:
    backgroundColor: "{colors.primary-soft}"
    textColor: "{colors.on-primary-soft}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  badge-faltou:
    backgroundColor: "{colors.warning-soft}"
    textColor: "{colors.on-warning-soft}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  badge-sumido:
    backgroundColor: "{colors.warning-soft}"
    textColor: "{colors.on-warning-soft}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  badge-cancelado:
    backgroundColor: "{colors.surface-disabled}"
    textColor: "{colors.muted}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  badge-nao-salvo:
    backgroundColor: "{colors.error-soft}"
    textColor: "{colors.error}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 6px
  day-chip:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.md}"
    width: 48px
    height: 64px
  day-chip-active:
    backgroundColor: "{colors.inverse}"
    textColor: "{colors.on-inverse}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.md}"
    width: 48px
    height: 64px
  filter-pill:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 12px
    height: 40px
  filter-pill-active:
    backgroundColor: "{colors.inverse}"
    textColor: "{colors.on-inverse}"
    typography: "{typography.label-sm}"
    rounded: "{rounded.full}"
    padding: 12px
    height: 40px
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 16px
    height: 52px
  input-error-message:
    textColor: "{colors.error}"
    typography: "{typography.caption}"
  search-field:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.full}"
    padding: 16px
    height: 48px
  caption:
    textColor: "{colors.muted}"
    typography: "{typography.caption}"
  divider:
    backgroundColor: "{colors.border}"
    height: 1px
  tab-bar:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.muted}"
    typography: "{typography.label-sm}"
    height: 64px
  tab-item-active:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.primary}"
    typography: "{typography.label-sm}"
  fab-add:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.on-primary}"
    rounded: "{rounded.full}"
    size: 60px
  bottom-sheet:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.lg}"
    padding: 24px
  snackbar:
    backgroundColor: "{colors.inverse}"
    textColor: "{colors.on-inverse}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    padding: 16px
  snackbar-action:
    backgroundColor: "{colors.inverse}"
    textColor: "{colors.accent-on-inverse}"
    typography: "{typography.label-md}"
    height: 48px
  banner-offline:
    backgroundColor: "{colors.inverse}"
    textColor: "{colors.on-inverse}"
    typography: "{typography.caption}"
    padding: 8px
    height: 32px
  swipe-action-cancel:
    backgroundColor: "{colors.error}"
    textColor: "{colors.on-error}"
    typography: "{typography.label-sm}"
    width: 88px
  swipe-action-reschedule:
    backgroundColor: "{colors.inverse}"
    textColor: "{colors.on-inverse}"
    typography: "{typography.label-sm}"
    width: 88px
---

## Overview

Treinou é ferramenta de trabalho, não app de lifestyle. Quem usa é o personal em pé no vestiário, com uma mão, olhando de relance entre um aluno e outro, muitas vezes sob luz fluorescente forte ou no sol do parque. A sensação: **rápido, firme e confiável**. Uma frase: o app tem que parecer um cronômetro bom, e não uma rede social de academia.

Esta identidade é uma proposta construída a partir das personas. Dá para trocar a cor de ação e as fontes sem mexer na estrutura, desde que o contraste e os tamanhos mínimos se mantenham.

## Colors

- **primary (verde `#0B7A3E`)**: só para a ação que conclui algo. "Presente", "Salvar", "Agendar", o botão "+" e a aba ativa. Na Agenda ele aparece uma vez por card não registrado; em qualquer outra tela, no máximo um botão primário visível.
- **primary-pressed**: estado pressionado do verde. Nunca usado como cor de repouso.
- **primary-soft / on-primary-soft**: confirmação calma. Selo "Presente", botão secundário ("Faltou", "Já tenho conta", "Registrar treino avulso") e fundo do avatar com iniciais (cor fixa para todo aluno, sem cor por pessoa).
- **background (`#F3F4EF`)**: fundo de todas as telas. Um off-white levemente quente que diminui o brilho sob luz de academia.
- **surface (branco)**: cards, folhas inferiores, campos e barra de abas. O contraste entre background e surface separa os blocos sem precisar de sombra.
- **on-surface / on-background (`#14181F`)**: todo texto principal. Contraste acima de 16:1.
- **muted (`#5A6270`)**: texto secundário (local, "Há 2 dias", legenda), cards já registrados e itens desabilitados. Contraste acima de 5:1 em branco e no background.
- **border**: só divisórias entre linhas da lista de alunos.
- **warning-soft / on-warning-soft**: pendência que pede atenção, sem ser erro. Selos "Faltou" e "Sumido".
- **error / error-soft**: erro e ação destrutiva. Mensagem de campo, selo "Não salvo", botão "Sair mesmo assim" e a ação "Cancelar" ao deslizar o card.
- **inverse / on-inverse / accent-on-inverse**: camada temporária por cima de tudo. Aviso com "Desfazer", faixa "Sem internet", dia selecionado na faixa e filtro ativo. O verde claro `accent-on-inverse` é só para a ação dentro do aviso escuro.

Verde nunca indica estado de dado (só o selo suave). Vermelho nunca aparece em tela sem erro ou ação destrutiva.

## Typography

- **Barlow Semi Condensed** para números e títulos de tela: estreita, legível de longe e com cara de placar. **Inter** para todo o resto.
- `display` (28px): título de tela ("Alunos") e iniciais do avatar grande.
- `time` (26px): horário do card da Agenda. É o maior texto da lista, porque é o que o Carlos procura primeiro.
- `title` (20px): títulos de seção ("Histórico", "Horários fixos") e nome do aluno no perfil.
- `body-strong` (16px, 600): nome do aluno em card e lista.
- `body-md` (16px): texto corrido, campos, observações, aviso.
- `label-md` (16px, 600): botões e links.
- `label-sm` e `caption` (14px): selos, faixa de dias, abas, texto secundário.
- Tamanho mínimo: 14px. Nada menor, nem em legenda. Campos de texto sempre com 16px para o iOS não dar zoom.
- Respeitar o tamanho de fonte do sistema até 130%; acima disso, quebrar linha em vez de cortar o nome.

## Layout

- Uma coluna, pensada para celular de 360 a 430 px de largura. Margem lateral de 16px (`spacing.md`).
- Espaço entre cards da Agenda: 8px (`spacing.sm`). Entre seções de uma tela: 24px (`spacing.lg`). Topo de tela até o título: 32px (`spacing.xl`) abaixo da área segura.
- **Zona do polegar:** ações primárias ficam no terço inferior da tela ou na borda direita do card. Botões fixos na base respeitam a área segura e ficam 16px acima dela.
- Alvo de toque mínimo de 48 x 48 px, mesmo quando o desenho é menor. Entre dois alvos, pelo menos 8px.
- Barra de abas fixa de 64px com o "+" central. A Agenda rola por baixo dela; o último card nunca fica escondido atrás da barra.
- Folhas inferiores ocupam no máximo 90% da altura e abrem já com o campo principal visível acima do teclado.
- Tablet e telas largas: o conteúdo para em 560px de largura, centralizado. Sem layout de desktop no MVP.

## Elevation & Depth

- Visual plano. A hierarquia vem do contraste entre `background` e `surface`, não de sombra.
- Cards e lista: sem sombra, sem borda.
- Só duas camadas flutuam, e só elas têm sombra: a folha inferior (sombra suave para cima, com o fundo escurecido a 40% de preto) e o aviso escuro na base (sombra curta de 8px).
- O botão "+" fica no nível da barra de abas, sem sombra própria.
- Foco de teclado e leitor de tela: contorno de 2px na cor `primary`, afastado 2px do elemento.

## Shapes

- Cantos de 12px (`rounded.md`) para botões, cards, campos e faixa de dias. 20px (`rounded.lg`) só no topo da folha inferior. Círculo (`rounded.full`) para avatar, selos, filtros, busca e o "+".
- Ícones de linha, traço de 2px, 24px, uma única biblioteca (Lucide). Ícone sempre acompanhado de texto, exceto voltar, busca e o "+".
- Ilustração só nos estados vazios: traço simples na cor `muted`, sem pessoas desenhadas com corpo "fitness" idealizado.
- Fotos de aluno sempre recortadas em círculo. Sem foto, iniciais (até duas letras) no avatar.

## Components

- **button-primary**: "Salvar", "Agendar", "Criar conta", "Salvar aluno". Pressionado usa `button-primary-pressed`. Desabilitado usa `button-primary-disabled` e só aparece enquanto o formulário não tem os campos obrigatórios. Carregando: o texto vira "Salvando..." e o botão não muda de tamanho. Erro: o botão volta ao normal e a mensagem aparece no campo.
- **button-presente**: a versão compacta do primário dentro do card da Agenda, sempre à direita, 112 x 48 px. Ao tocar, vira o `badge-presente` em menos de 300 ms. Em dias futuros não é renderizado.
- **button-secondary**: segunda opção ao lado ou abaixo do primário ("Faltou", "Registrar treino avulso", "Já tenho conta"). Nunca dois secundários sem um primário na mesma tela, exceto o par "Presente / Faltou" da folha Registrar treino, em que o selecionado vira primário.
- **button-destructive**: só em confirmação de perda ("Sair mesmo assim", "Descartar").
- **link**: ações de texto ("Esqueci a senha", "Ver mais", "Editar").
- **card-agenda**: horário (`card-agenda-time`) à esquerda, avatar, nome e local no meio, `button-presente` à direita. Pressionado escurece o fundo para `background`. Registrado usa `card-agenda-registrado` com o selo no lugar do botão. Não salvo: mantém o estado e mostra `badge-nao-salvo`.
- **swipe-action-reschedule / swipe-action-cancel**: aparecem ao deslizar o card para a esquerda, com 88px cada. "Cancelar" à direita, mais longe do polegar.
- **list-item-aluno**: avatar, nome, próximo e último treino, selo "Sumido" quando for o caso. Separado por `divider`.
- **avatar / avatar-lg**: 48px na lista e na Agenda, 88px no perfil.
- **badge-presente, badge-faltou, badge-sumido, badge-cancelado, badge-nao-salvo**: sempre com texto, nunca só cor.
- **day-chip / day-chip-active**: faixa de dias da Agenda. Hoje tem um ponto de 4px abaixo do número quando não está selecionado.
- **filter-pill / filter-pill-active**: "Ativos", "Sumidos", "Inativos" na aba Alunos.
- **input**: rótulo acima em `label-sm`, nunca só placeholder. Foco: contorno de 2px `primary`. Erro: contorno de 2px `error` e `input-error-message` abaixo. Desabilitado: fundo `surface-disabled`.
- **search-field**: topo da aba Alunos e do seletor de aluno, com ícone de lupa e botão de limpar.
- **tab-bar / tab-item-active / fab-add**: três itens, "Hoje", "+" e "Alunos". A aba ativa muda a cor do ícone e do texto para `primary`.
- **bottom-sheet**: Registrar treino, Agendar treino, Menu Adicionar, pergunta pós-cadastro. Alça de arraste no topo.
- **snackbar / snackbar-action**: aviso de 6 segundos com no máximo duas ações ("Observação", "Desfazer"). Um por vez; o novo substitui o anterior.
- **banner-offline**: faixa de 32px no topo, abaixo da área segura, em todas as telas enquanto não houver conexão.
- **caption, screen, screen-title, section-title**: texto secundário, fundo de tela e os dois níveis de título.

## Do's and Don'ts

- Do: manter um único botão verde por bloco de decisão. Se tudo é verde, nada é.
- Do: escrever rótulo de botão como verbo de ação curto ("Salvar", "Agendar"), nunca "OK" ou "Confirmar".
- Do: mostrar o selo com texto ("Faltou") além da cor; parte dos personais vai usar o app no sol.
- Do: usar "Desfazer" no aviso em vez de janela de confirmação para registrar, cancelar e inativar.
- Do: testar cada tela com o polegar direito num celular de 6,5", com brilho no máximo.
- Don't: usar texto menor que 14px ou cinza mais claro que `muted`.
- Don't: colocar ação importante no canto superior esquerdo.
- Don't: usar gradiente, foto de fundo, ilustração de corpo atlético ou linguagem de rede social ("curtir", "seguir", "postar").
- Don't: criar cor nova fora deste arquivo. Se faltar, proponha o token e atualize o DESIGN.md.
- Don't: usar sombra em card ou lista. Sombra é só para o que flutua.
