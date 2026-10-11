# [Nome do produto]

[O produto em duas frases: o que faz e para quem.]

## Antes de mexer em qualquer coisa

Leia, nesta ordem:

1. `docs/contexto.md`: problema, público, escopo, o que não é, critério de sucesso e de morte.
2. `docs/personas.md`: quem usa e em que situação. Em conflito, otimize para a persona principal.
3. `docs/fluxos.md`: telas, fluxos e estados.
4. `docs/estruturadedados.md`: entidades, campos e regras de negócio.
5. `DESIGN.md`: cores, tipografia, espaçamento e componentes. Todo elemento visual segue este arquivo.
6. `docs/integracoes.md`: autenticação, banco, APIs e infraestrutura.
7. `docs/metricas.md`: eventos que precisam ser registrados.
8. `docs/decisoes.md`: decisões técnicas já tomadas. Não reabra sem motivo novo.

## Stack e comandos

- Stack: [framework, banco, hospedagem]
- Instalar: `[comando]`
- Rodar: `[comando]`
- Testar: `[comando]`

## Regras de trabalho

- Construa uma funcionalidade por vez, na ordem do escopo em `docs/contexto.md`.
- Nada fora do escopo sem confirmar antes.
- Cor, fonte e espaçamento vêm do `DESIGN.md`. Não invente valor novo; se precisar, proponha e atualize o arquivo.
- Mudou dado, tela, integração ou tecnologia? Atualize o doc correspondente na mesma entrega.
- Decisão técnica relevante vai para `docs/decisoes.md` com data, alternativa descartada e motivo.
