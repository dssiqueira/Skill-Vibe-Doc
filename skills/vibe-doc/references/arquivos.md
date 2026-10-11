# O que vai em cada arquivo

## Regras de escrita (valem para todos)

- **Escreva para quem assume, não para quem pergunta.** Cada frase deve fechar uma decisão que a IA teria que chutar.
- **Denso, não longo.** Lista e frase curta. Se um parágrafo não muda o que a IA vai construir, corte.
- **Concreto sempre.** "Personal com 15 alunos que usa o celular com uma mão entre atendimentos" vale mais que "profissionais da área fitness".
- **Diga o que não é.** O escopo negativo evita metade do retrabalho.
- **Número quando existir.** Prazo, volume, limite, meta, tempo de tela.
- **Nada de placeholder.** Se não sabe, pergunte. Se é sugestão sua, marque `<!-- sugestão: confirmar -->`.
- **Um assunto por arquivo.** Cor não entra em `fluxos.md`. Tela não entra no DESIGN.md.

## AGENTS.md (raiz)

A porta de entrada que qualquer agente lê primeiro. Cabe em uma tela.
- O produto em duas frases.
- Mapa dos arquivos, com uma linha sobre cada um.
- A stack principal e os comandos do projeto (instalar, rodar, testar), quando existirem.
- Regras de trabalho: ler os docs antes de mudar algo relevante, atualizar os docs depois, registrar decisão técnica em `docs/decisoes.md`, seguir o DESIGN.md para qualquer coisa visual.

## DESIGN.md (raiz)

A identidade visual em formato que a máquina lê e a pessoa entende. Detalhes em `design-md.md`.

## docs/contexto.md

- **Problema**: quem sofre, com o quê, quanto custa hoje.
- **Solução**: o que o produto faz, em uma situação real de uso.
- **Audiência principal**: um perfil, não uma lista.
- **Escopo do MVP**: 3 a 6 itens.
- **O que NÃO é**: 3 a 6 itens.
- **Critério de sucesso**: número e prazo ("80% dos personais registram presença em menos de 10 segundos no primeiro mês").
- **Critério de morte**: o número que, se não for atingido no prazo, faz parar, pivotar ou revisar. Quem propõe define antes de construir.

## docs/personas.md

Uma a três personas. Para cada: perfil curto, contexto de uso (onde, quando, com que aparelho, com quanto tempo), comportamento, frustrações atuais, o que evita. Termine dizendo qual é a persona principal e que, em conflito, otimiza-se para ela.

## docs/estruturadedados.md

Para cada entidade: o que representa, campos com tipo e obrigatoriedade, relacionamentos. Depois, regras de negócio agrupadas por entidade. Pense em planilha: cada entidade é uma aba, cada campo é uma coluna.

## docs/fluxos.md

O que existe no produto e por onde a pessoa anda. Sem cor, sem fonte, sem pixel.
- **Princípios de experiência** (3 a 5): por exemplo, "máximo dois toques para a ação mais frequente".
- **Mapa de telas**: lista de todas as telas com objetivo em uma linha.
- **Cada tela**: objetivo, hierarquia do conteúdo (do mais importante ao menos), ações e interações.
- **Fluxos principais**: passo a passo numerado, com tempo esperado quando importa.
- **Estados**: vazio, carregando, erro, sem conexão, sem permissão.

## docs/metricas.md

- Métricas de negócio (o que diz se o produto deu certo), com fórmula e meta.
- Métricas de uso da funcionalidade principal.
- Eventos a registrar, com nome em `snake_case` e campos.
- O que não entra no MVP.

## docs/integracoes.md

Autenticação, banco e regras de acesso, armazenamento de arquivos, APIs externas, pagamentos, notificações, ambiente e deploy, monitoramento. Para cada item: o que usar, por quê, e o que fica para depois do MVP.

## docs/decisoes.md

Registro curto de decisões técnicas, a mais recente em cima. Cada entrada:
- data e título;
- contexto em uma frase;
- decisão;
- alternativas descartadas e por quê;
- nível de autonomia quando envolve IA: sem IA, fluxo determinístico, fluxo com etapa de IA, agente de tarefa ou agente autônomo, e por que o degrau mais baixo não bastou;
- onde entra o humano, quando aplicável.

Regra: entre duas soluções que resolvem a mesma dor, vence a mais simples.
