# Métricas

## Métricas de negócio

### Adoção do canal
**O que medir:** quanto dos pedidos de TI entra pelo Balcão TI.
**Por que importa:** é o critério de sucesso e de morte. Se o email continuar sendo o canal, a ferramenta não resolveu nada.
**Como calcular:** chamados com `aberto_por_id = solicitante_id` dividido pelo total de chamados no período (os abertos "em nome de" representam pedidos que chegaram por fora).
**Meta:** 80% em 90 dias. Abaixo de 50% em 90 dias aciona o critério de morte.

### Tempo de resolução por categoria
**O que medir:** tempo mediano entre `criado_em` e `resolvido_em`, separado por categoria.
**Por que importa:** mostra onde o TI trava e sustenta pedido de contratação.
**Como calcular:** mediana de `resolvido_em - criado_em` dos chamados resolvidos no período, em horas úteis (8h às 18h, segunda a sexta).
**Meta:** Acesso abaixo de 4 horas úteis; Suporte abaixo de 1 dia útil; Equipamento sem meta no MVP (depende de compra).

### Resolução sem idas e vindas
**O que medir:** chamados resolvidos que nunca passaram por `aguardando_solicitante`.
**Por que importa:** indica se o formulário coleta informação suficiente.
**Como calcular:** resolvidos sem nenhum `status_alterado` para `aguardando_solicitante` dividido pelo total de resolvidos.
**Meta:** 70%.

### Carga por analista
**O que medir:** chamados resolvidos e em andamento por analista no período.
**Por que importa:** distribuir a fila e mostrar à coordenação quem está sobrecarregado.
**Como calcular:** contagem de `chamado_resolvido` e de chamados `em_andamento` agrupada por `analista_id`.
**Meta:** nenhum analista com mais que o dobro da média do time em andamento.

### Volume
**O que medir:** chamados abertos por semana e por mês, por categoria.
**Por que importa:** dimensionar o time e ver sazonalidade (fechamento contábil, admissões).
**Como calcular:** contagem de `chamado_aberto` por período.
**Meta:** sem meta; é acompanhamento.

## Métricas de uso

### Tempo para abrir um chamado
**O que medir:** quanto o solicitante leva entre abrir o formulário e enviar.
**Registrar:** evento `formulario_iniciado` com `usuario_id` e o `chamado_aberto` seguinte do mesmo usuário; a diferença entre os dois.
**Meta:** mediana abaixo de 3 minutos.

### Calibração de prioridade
**O que medir:** percentual de chamados abertos como `critica` e quanto deles o analista rebaixou.
**Registrar:** evento `chamado_aberto` com `prioridade`, e `prioridade_alterada` com `valor_anterior` e `valor_novo`.
**Meta:** até 5% dos chamados abertos como crítico; se mais da metade dos críticos for rebaixada, revisar os textos de prioridade do formulário.

### Taxa de cancelamento
**O que medir:** chamados cancelados sobre o total aberto.
**Registrar:** evento `status_alterado` com `valor_novo = cancelado` e quem cancelou.
**Meta:** abaixo de 10%. Acima disso, investigar pedidos mal direcionados.

## Eventos a registrar
- `formulario_iniciado`: solicitante ou analista abre a tela Novo chamado. Campos: `usuario_id`, `perfil`.
- `chamado_aberto`: chamado criado. Campos: `chamado_id`, `categoria`, `prioridade`, `solicitante_id`, `aberto_por_id`, `tem_anexo`, `chamado_origem_id`.
- `chamado_atribuido`: responsável definido ou trocado. Campos: `chamado_id`, `analista_id`, `analista_anterior_id`.
- `status_alterado`: qualquer mudança de status. Campos: `chamado_id`, `valor_anterior`, `valor_novo`, `autor_id`, `criado_em`.
- `prioridade_alterada`: analista muda a prioridade. Campos: `chamado_id`, `valor_anterior`, `valor_novo`, `autor_id`.
- `comentario_adicionado`: comentário enviado. Campos: `chamado_id`, `autor_id`, `visivel_para_solicitante`.
- `chamado_resolvido`: status vira `resolvido`. Campos: `chamado_id`, `categoria`, `analista_id`, `tempo_resolucao_horas_uteis`.

Todos os eventos são gravados na entidade Evento (`docs/estruturadedados.md`), no mesmo banco, pela mesma função ou transação que executa a ação. Nada de ferramenta externa de analytics.

## Fora do MVP
- Tempo que o analista passa em cada tela (privacidade e clima de vigilância).
- Comportamento de navegação dos solicitantes.
- Pesquisa de satisfação após o fechamento (entra se a resolução sem idas e vindas ficar abaixo da meta).
- SLA e alerta de prazo estourado.
