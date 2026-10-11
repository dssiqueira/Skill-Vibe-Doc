# DESIGN.md

Padrão aberto do Google Labs, nascido no Stitch e publicado em abril de 2026 (Apache 2.0, ainda em alpha: confira mudanças em https://github.com/google-labs-code/design.md). Faz para o design o que o AGENTS.md faz para o código: um arquivo na raiz que qualquer agente lê para manter o produto com a mesma cara em todas as telas.

O arquivo tem duas camadas:

1. **Frontmatter YAML** com os tokens: o que a máquina aplica.
2. **Corpo em markdown** com o porquê: o que orienta o julgamento quando o token não basta.

## Frontmatter

```yaml
---
version: alpha
name: Nome do produto          # obrigatório
description: Uma linha sobre a identidade visual
colors:
  primary: "#1A1C1E"           # formato recomendado: #RRGGBB
  on-primary: "#FFFFFF"
  surface: "#FFFFFF"
  on-surface: "#1A1C1E"
  accent: "#E38B3D"
  error: "#C62828"
typography:
  display:
    fontFamily: Inter
    fontSize: 40px             # unidades aceitas: px, em, rem
    fontWeight: 700
    lineHeight: 1.1            # número sem unidade multiplica o fontSize
    letterSpacing: -0.02em
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: 400
    lineHeight: 1.5
  label-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: 600
    lineHeight: 1.2
rounded:
  sm: 4px
  md: 8px
  full: 999px
spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 40px
components:
  button-primary:
    backgroundColor: "{colors.primary}"   # referência a outro token
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.md}"
    padding: 12px
    height: 48px
---
```

Regras:
- Chaves de topo aceitas: `version`, `name`, `description`, `colors`, `typography`, `rounded`, `spacing`, `components`.
- Propriedades de componente aceitas: `backgroundColor`, `textColor`, `typography`, `rounded`, `padding`, `size`, `height`, `width`. Variante e estado viram componente próprio (`button-primary-hover`, `button-primary-disabled`).
- Referências usam chaves: `"{colors.primary}"`. Fora de `components`, aponte para um valor, não para um grupo.
- Use nomes de papel, não de cor: `primary`, `surface`, `on-surface`, `error`. "azul" não diz para que serve.
- Para cada cor de fundo, defina a cor do texto que vai em cima (`on-...`) e garanta contraste de pelo menos 4,5:1 para texto normal. O lint confere.

## Corpo

Seções `##` opcionais, mas as que existirem precisam vir nesta ordem e sem repetir:

1. `## Overview`: personalidade da marca, público, a sensação que o produto deve passar em três adjetivos e uma frase.
2. `## Colors`: o papel de cada cor e quando usar. Qual é a cor da ação principal e quantas vezes ela aparece por tela.
3. `## Typography`: hierarquia, quando usar cada estilo, tamanho mínimo.
4. `## Layout`: grid, larguras máximas, espaçamento entre blocos, comportamento no celular. É o layout visual; telas e fluxos ficam em `docs/fluxos.md`.
5. `## Elevation & Depth`: sombra, camadas, bordas.
6. `## Shapes`: cantos, ícones, ilustração.
7. `## Components`: cada componente com estados (padrão, hover, foco, desabilitado, erro).
8. `## Do's and Don'ts`: regras curtas que evitam os erros mais prováveis.

Escreva os títulos das seções exatamente assim, em inglês, para as ferramentas reconhecerem. O texto dentro delas vai no idioma da pessoa.

## Como montar sem identidade visual pronta

1. Parta das personas: quem usa com uma mão no celular precisa de alvo de toque de 48px e contraste alto; quem usa num escritório o dia inteiro precisa de densidade e tons calmos.
2. Escolha uma cor de ação e uma neutra. Mais cores só com papel claro.
3. Uma família tipográfica basta. Duas, no máximo.
4. Diga à pessoa que a identidade é uma proposta e o que ela pode trocar.

## Comandos (precisa de Node)

```bash
npx @google/design.md lint DESIGN.md                  # valida estrutura, referências e contraste
npx @google/design.md diff DESIGN.anterior.md DESIGN.md  # mostra o que mudou entre versões
npx @google/design.md export --format css-tailwind DESIGN.md  # gera tema para Tailwind
npx @google/design.md export --format dtcg DESIGN.md          # tokens no formato W3C
```

Se o projeto usa Tailwind, gere o tema a partir do DESIGN.md em vez de manter cores em dois lugares.
