# Contexto do produto

## Problema
Uma empresa de 600 colaboradores tem um time de TI com 4 analistas que recebe cerca de 250 pedidos por mês por email, WhatsApp, Teams e no corredor. Não existe fila única, histórico nem prioridade:
- pedidos se perdem (o analista estima que 1 em cada 10 só é lembrado quando o solicitante cobra);
- o solicitante não sabe o status e liga ou manda mensagem para perguntar, o que consome cerca de 1 hora por dia de cada analista;
- o analista não sabe o que é urgente e atende quem grita mais alto;
- não há dado para justificar contratação ou mostrar carga por pessoa.

## Solução
Uma ferramenta web interna, o Balcão TI, onde todo pedido de TI vira um chamado com categoria, prioridade, responsável e histórico.

Situação real: Marcos, do financeiro, perde o acesso à pasta de fechamento às 9h. Ele entra pelo login corporativo, clica em "Novo chamado", escolhe "Acesso", descreve em duas linhas e envia em menos de 3 minutos. Rafael, do TI, vê o chamado no topo da fila, atribui a si mesmo, libera o acesso e marca como resolvido. Marcos recebe um email avisando, sem ter perguntado nada a ninguém.

## Audiência principal
Colaborador não técnico (financeiro, comercial, RH) que abre um chamado poucas vezes por mês, pelo navegador do computador corporativo, e quer resolver o pedido sem aprender um sistema. Do outro lado, os 4 analistas de TI, que usam a ferramenta o dia inteiro.

## Escopo do MVP
1. Login com a conta Microsoft corporativa, perfil definido por grupo do Entra ID.
2. Abertura de chamado pelo solicitante (título, categoria, descrição, prioridade, anexo opcional) e abertura pelo analista em nome de um colaborador.
3. Lista "Meus chamados" e detalhe com status e comentários públicos para o solicitante.
4. Fila do analista com filtros, busca, atribuição, mudança de status e prioridade, e comentário público ou interno.
5. Emails automáticos nos eventos de `docs/integracoes.md`.
6. Painel com as métricas de `docs/metricas.md` para analistas e admin.

## O que NÃO é (pelo menos agora)
- Não é um ITSM completo: não substitui ServiceNow nem Jira Service Management, não tem CMDB, gestão de mudanças nem catálogo de serviços.
- Não tem SLA automático, cronômetro de prazo nem contrato de fornecedor.
- Não tem aprovação de compra, orçamento ou módulo financeiro. Pedido de equipamento é registrado; a compra segue o processo atual.
- Não é acessível fora da rede interna ou da VPN.
- Não tem app de celular. Funciona no navegador do celular, mas o desenho é para desktop.
- Não usa IA para classificar ou responder chamados (ver `docs/decisoes.md`).

## Restrições
- Interface em português brasileiro.
- Desktop primeiro (1280px ou mais). Celular só precisa não quebrar.
- Nenhum dado de chamado sai do ambiente aprovado pela empresa (Supabase em região São Paulo).

## Critério de sucesso
Em 90 dias após o lançamento, 80% dos pedidos de TI entram pelo Balcão TI (medido contra os pedidos que os analistas registram manualmente por terem chegado por outro canal) e o tempo mediano de resolução de chamados de "Acesso" fica abaixo de 4 horas úteis.

## Critério de morte
Se em 90 dias menos de 50% dos pedidos entrarem pela ferramenta, ou se os analistas voltarem a triar pelo email em mais de 2 dos 4 casos, o projeto para e a decisão é revista: contratar um ITSM pronto (Jira Service Management) em vez de manter ferramenta própria.
