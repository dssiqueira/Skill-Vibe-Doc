---
version: alpha
name: "[Nome do produto]"
description: "[A identidade visual em uma linha]"
colors:
  primary: "#000000"
  on-primary: "#FFFFFF"
  surface: "#FFFFFF"
  on-surface: "#000000"
  muted: "#6B7280"
  border: "#E5E7EB"
  success: "#15803D"
  error: "#B91C1C"
typography:
  display:
    fontFamily: Inter
    fontSize: 32px
    fontWeight: 700
    lineHeight: 1.15
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
  label-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: 600
    lineHeight: 1.2
rounded:
  sm: 4px
  md: 8px
  lg: 16px
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
    padding: 12px
    height: 48px
  card:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    rounded: "{rounded.lg}"
    padding: 16px
  input:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.on-surface}"
    typography: "{typography.body-md}"
    rounded: "{rounded.md}"
    height: 48px
  caption:
    textColor: "{colors.muted}"
    typography: "{typography.label-md}"
  divider:
    backgroundColor: "{colors.border}"
    height: 1px
  badge-success:
    backgroundColor: "{colors.success}"
    textColor: "{colors.on-primary}"
    typography: "{typography.label-md}"
    rounded: "{rounded.full}"
    padding: 4px
---

## Overview

[Personalidade da marca, público e a sensação que o produto passa. Três adjetivos e uma frase.]

## Colors

[Papel de cada cor. Qual é a cor da ação principal e quantas vezes ela aparece por tela.]

## Typography

[Hierarquia, quando usar cada estilo, tamanho mínimo de texto.]

## Layout

[Grid, largura máxima, espaçamento entre blocos, comportamento no celular. Telas e fluxos ficam em docs/fluxos.md.]

## Elevation & Depth

[Sombras, camadas e bordas.]

## Shapes

[Cantos, ícones, ilustração.]

## Components

[Cada componente com seus estados: padrão, hover, foco, desabilitado, erro.]

## Do's and Don'ts

- Do: [regra]
- Don't: [regra]
