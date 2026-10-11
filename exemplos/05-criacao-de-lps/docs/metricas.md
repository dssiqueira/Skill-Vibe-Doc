# Métricas

## Métricas de negócio

### Taxa de exportação
**O que medir:** gerações que viram HTML baixado.
**Por que importa:** é a prova de que a página saiu boa o bastante para ir ao ar. É o centro do critério de sucesso e do de morte.
**Como calcular:** páginas com `pagina_exportada` ÷ eventos `geracao_concluida`, por semana.
**Meta:** 40% em 90 dias. Abaixo de 20% em 90 dias aciona o critério de morte.

### Adoção de marca própria
**O que medir:** páginas exportadas com Marca importada ou montada, não tema padrão.
**Por que importa:** a promessa "com a cara da sua marca" é o diferencial frente a qualquer gerador genérico.
**Como calcular:** `pagina_exportada` com `marca_origem` em `importada` ou `gerada` ÷ total de `pagina_exportada`.
**Meta:** 30% em 90 dias.

### Conversão free para pro
**O que medir:** usuários free que assinam o pro.
**Por que importa:** paga a conta da IA e da infraestrutura.
**Como calcular:** assinaturas confirmadas pelo webhook do Stripe no mês ÷ usuários free ativos no mês.
**Meta:** 4% em 90 dias. Abaixo de 1,5% revisa o modelo de cobrança.

### Custo de IA por página exportada
**O que medir:** quanto a IA custa para cada página que vai ao ar.
**Por que importa:** página regerada várias vezes e nunca exportada é custo sem receita.
**Como calcular:** soma de `custo_estimado_centavos` de todas as gerações do mês ÷ páginas exportadas no mês.
**Meta:** até R$ 0,40 por página exportada.

## Métricas de uso

### Tempo do briefing à exportação
**O que medir:** fluidez do fluxo principal.
**Registrar:** diferença entre `briefing_iniciado` e `pagina_exportada` da mesma sessão. Meta: mediana abaixo de 5 minutos.

### Quanto do texto a IA acerta
**O que medir:** proporção de blocos reescritos antes de exportar e quais campos mais mudam.
**Registrar:** evento `texto_editado` com `secao` e `campo`; por página, blocos editados ÷ total de blocos. Acima de 50% em mais de 60% das páginas exportadas aciona o critério de morte.

### Tempo de geração
**O que medir:** se a geração cabe no limite de 15 segundos.
**Registrar:** `geracao_concluida` com `tempo_ms`. Meta: p90 abaixo de 15 segundos.

### Saúde da importação de marca
**O que medir:** quantos DESIGN.md chegam quebrados e por quê.
**Registrar:** `marca_lint_falhou` com `regras_violadas` (lista de nomes de regra do lint, sem o conteúdo do arquivo).

## Eventos a registrar
- `briefing_iniciado`: toque em "Criar minha página" ou "Nova página". Campos: `sessao_id`, `logado` (bool).
- `marca_importada`: DESIGN.md importado passou no lint. Campos: `marca_id`, `warnings` (inteiro).
- `marca_gerada`: marca montada pelos 4 campos. Campos: `marca_id`, `contraste_corrigido` (bool), `tem_logo` (bool).
- `marca_lint_falhou`: DESIGN.md importado com erro. Campos: `regras_violadas`, `corrigido_automaticamente` (bool).
- `geracao_concluida`: página pronta. Campos: `pagina_id`, `tempo_ms`, `tom`, `objetivo_cta`, `marca_origem`, `custo_estimado_centavos`.
- `geracao_falhou`: erro ou recusa. Campos: `motivo` (`timeout | json_invalido | recusa_conteudo | erro_api`), `tempo_ms`.
- `texto_editado`: saída de um campo editado no painel. Campos: `pagina_id`, `secao`, `campo`.
- `pagina_regerada`: "Gerar novamente" confirmado. Campos: `pagina_anterior_id`.
- `pagina_exportada`: HTML baixado. Campos: `pagina_id`, `marca_origem`, `blocos_editados`, `blocos_total`, `removeu_prova_social` (bool).
- `conta_criada`: cadastro concluído no modal. Campos: `metodo` (`google | email`), `veio_de_geracao` (bool).
- `limite_atingido`: free tenta gerar sem crédito. Campos: `geracoes_no_mes`.
- `assinatura_iniciada`: toque em "Assinar pro". Campos: `origem` (`limite | planos`).

## Fora do MVP
- Conteúdo dos briefings, dos textos gerados e dos textos editados (privacidade: medimos que mudou, nunca o quê).
- Conteúdo dos DESIGN.md importados.
- Conversão das páginas publicadas (o produto não hospeda e não injeta script de rastreio no HTML exportado).
- Teste A/B de prompt; volta quando houver 1.000 gerações por semana.
