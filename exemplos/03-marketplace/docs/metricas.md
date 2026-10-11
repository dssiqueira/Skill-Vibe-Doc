# Métricas

*Marketplace se mede dos dois lados. Demanda sem oferta vira "0 profissionais"; oferta sem demanda vira app que ninguém abre. As metas abaixo são as do critério de sucesso em `contexto.md`.*

## Métricas de negócio

### Liquidez do pedido
**O que medir:** pedidos que recebem pelo menos 1 proposta em até 24 horas.
**Por que importa:** é a promessa do produto para a Cláudia. Abaixo disso ela volta para o grupo do prédio.
**Como calcular:** pedidos com `proposta_enviada` em até 24 h de `pedido_aberto` ÷ pedidos com `pedido_aberto` no período (coorte por semana de abertura).
**Meta:** 60% no dia 90. Abaixo de 30% aciona o critério de morte.

### Taxa de match
**O que medir:** pedidos que chegam a `em_andamento`.
**Por que importa:** proposta que ninguém aceita não gera serviço nem avaliação.
**Como calcular:** pedidos com `proposta_aceita` ÷ pedidos com `pedido_aberto`, mesma coorte.
**Meta:** 30% no dia 90.

### Profissionais ativos por semana
**O que medir:** profissionais com pelo menos 1 `proposta_enviada` nos últimos 7 dias.
**Por que importa:** é a oferta real, não a cadastrada.
**Como calcular:** contagem distinta de `profissional_id` em `proposta_enviada`, janela móvel de 7 dias.
**Meta:** 50 no dia 90. Abaixo de 20 aciona o critério de morte.

### Tempo até a primeira proposta
**O que medir:** mediana do tempo entre `pedido_aberto` e a primeira `proposta_enviada`, separada por `urgente`.
**Por que importa:** a promessa de tela é "até 2 horas".
**Meta:** mediana abaixo de 2 h para urgentes e de 8 h para os demais.

## Métricas de uso

### Conversão da consulta de cobertura
**O que medir:** quem consulta cobertura e chega a publicar pedido; e quantas consultas dão 0 profissionais (onde falta oferta).
**Registrar:** evento `cobertura_consultada` com `cep_prefixo` (5 dígitos), `categoria`, `total_profissionais`.

### Abandono do formulário de pedido
**O que medir:** quem começa Novo pedido e não publica. Meta: abaixo de 35%.
**Registrar:** `pedido_formulario_iniciado` e `pedido_aberto`, ligados por `sessao_id`.

### Pedidos por categoria
**O que medir:** demanda por tipo de serviço, para decidir onde recrutar profissional.
**Registrar:** `pedido_aberto` com `categoria`.

### Cadastro de profissional concluído
**O que medir:** quem escolhe "Quero oferecer serviços" e termina os 3 passos. Meta: acima de 70%.
**Registrar:** `profissional_cadastro_concluido` com `categorias`, `raio_km`, `tem_foto`.

### Avaliação após conclusão
**O que medir:** pedidos concluídos que recebem avaliação. Meta: acima de 60%.
**Registrar:** `pedido_concluido` e `avaliacao_registrada`.

## Eventos a registrar

Todos com `usuario_id` (quando houver), `tipo_usuario` e `criado_em`.

- `cobertura_consultada`: morador ou visitante vê o resultado no Início público. Campos: `cep_prefixo`, `categoria`, `total_profissionais`.
- `cadastro_concluido`: código SMS confirmado e nome e email salvos na tela Entrar. Campos: `tipo`.
- `profissional_cadastro_concluido`: fim do passo 3 do Cadastro do profissional. Campos: `categorias`, `raio_km`, `tem_foto`.
- `pedido_formulario_iniciado`: abertura de Novo pedido. Campos: `categoria`, `origem` (`inicio_publico` | `atalho_categoria` | `publicar_de_novo`), `sessao_id`.
- `pedido_aberto`: "Publicar pedido" com sucesso. Campos: `pedido_id`, `categoria`, `urgente`, `tem_data_preferida`, `profissionais_notificados`, `sessao_id`.
- `pedido_visualizado_profissional`: profissional abre o detalhe de um pedido. Campos: `pedido_id`, `distancia_km`.
- `proposta_enviada`: "Enviar proposta" com sucesso. Campos: `pedido_id`, `profissional_id`, `valor_min`, `valor_max`, `prazo_execucao`, `minutos_desde_abertura`.
- `proposta_aceita`: confirmação no modal de aceite. Campos: `pedido_id`, `proposta_id`, `profissional_id`, `posicao_na_lista`, `total_propostas`, `minutos_desde_abertura`.
- `contato_aberto`: toque em "Chamar no WhatsApp" ou "Ligar", dos dois lados. Campos: `pedido_id`, `canal` (`whatsapp` | `telefone`), `lado`.
- `pedido_concluido`: "Marcar como concluído". Campos: `pedido_id`, `categoria`, `horas_desde_aceite`.
- `pedido_cancelado`: confirmação de cancelamento. Campos: `pedido_id`, `status_anterior`, `total_propostas`.
- `pedido_expirado`: job de 72 horas. Campos: `pedido_id`, `total_propostas`.
- `proposta_cancelada`: confirmação em Minhas propostas. Campos: `proposta_id`, `pedido_id`.
- `avaliacao_registrada`: "Enviar avaliação". Campos: `pedido_id`, `avaliado_id`, `nota`, `tem_comentario`.
- `disponibilidade_alterada`: interruptor em Pedidos na região. Campos: `disponivel`.

## Fora do MVP

- NPS separado por lado (pesquisa entra depois de 100 pedidos concluídos).
- Receita, comissão e ticket médio: não há pagamento na plataforma.
- Se o serviço aconteceu de fato fora do app além do "Marcar como concluído".
- Navegação dentro do perfil do profissional (tempo na tela, fotos vistas): não registrar, por privacidade de quem está escolhendo.
- CEP completo e endereço em eventos: só os 5 primeiros dígitos do CEP.
