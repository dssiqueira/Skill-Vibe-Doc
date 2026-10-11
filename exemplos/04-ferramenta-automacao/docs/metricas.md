# Métricas

*Toda métrica sai da tabela LogAuditoria e dos timestamps de Onboarding e EtapaOnboarding. Não há ferramenta de analytics de navegação.*

## Métricas de negócio

### Tempo interno de onboarding
**O que medir:** tempo do início ao `concluido`, descontada a espera pela assinatura do cliente.
**Por que importa:** é o tempo que a empresa controla; é o critério de sucesso.
**Como calcular:** mediana semanal de `(concluido_em - iniciado_em) - (contrato_assinado_em - conclusão da etapa envio_contrato)`, em horas úteis.
**Meta:** abaixo de 2 horas úteis em até 60 dias de produção.

### Tempo total até o cliente ter acesso
**O que medir:** do início ao `concluido`, sem desconto.
**Por que importa:** é o que o cliente sente. Hoje leva de 3 a 5 dias úteis.
**Como calcular:** mediana semanal de `concluido_em - iniciado_em`, em dias úteis.
**Meta:** abaixo de 2 dias úteis.

### Taxa de onboardings com erro
**O que medir:** onboardings que tiveram pelo menos um `erro_detectado`.
**Por que importa:** mostra a estabilidade das integrações.
**Como calcular:** onboardings com algum `erro_detectado` / onboardings iniciados, por mês.
**Meta:** abaixo de 10%.

### Etapa com maior taxa de erro
**O que medir:** contagem de `erro_detectado` por `etapa`.
**Por que importa:** diz onde investir manutenção (e se o Sistema 3 merece automação).
**Como calcular:** `erro_detectado` por etapa / execuções da etapa, por mês.
**Meta:** nenhuma etapa automática acima de 5%.

### Adoção
**O que medir:** clientes novos que passaram pela ferramenta.
**Por que importa:** se a planilha continuar em paralelo, a ferramenta não substituiu o processo (critério de morte).
**Como calcular:** `onboarding_iniciado` no mês / contratos fechados no mês informados pelo comercial.
**Meta:** 100% no segundo mês.

## Métricas de uso

### Tempo de preenchimento do formulário
**O que medir:** do clique em "+ Novo onboarding" à confirmação.
**Registrar:** evento `onboarding_iniciado` com `segundos_formulario`.
**Meta:** mediana abaixo de 3 minutos.

### Tempo de resposta na etapa manual
**O que medir:** de a etapa 5 virar `aguardando_humano` a "Marcar como feito".
**Registrar:** evento `etapa_manual_concluida` com `minutos_em_espera`.
**Meta:** mediana abaixo de 30 minutos em horário comercial.

### Tempo de assinatura do cliente
**O que medir:** de `contrato_enviado` a `contrato_assinado`. É comportamento do cliente, não falha técnica.
**Registrar:** evento `contrato_assinado` com `horas_desde_envio`.

### Destraves manuais
**O que medir:** quantas vezes a Fernanda precisa clicar em "Tentar novamente".
**Registrar:** evento `tentativa_manual` com `etapa`.

## Eventos a registrar

Todos gravados em LogAuditoria, com `onboarding_id`, `executado_por` e `criado_em`.

- `onboarding_iniciado`: confirmação no modal de Novo onboarding. Campos: `plano`, `comercial_id`, `segundos_formulario`.
- `contrato_enviado`: etapa 1 concluída. Campos: `id_envelope`.
- `lembrete_assinatura_enviado`: clique em "Reenviar lembrete" no Detalhe. Campos: `dias_desde_envio`.
- `contrato_assinado`: webhook da D4Sign recebido e validado. Campos: `horas_desde_envio`.
- `acesso_criado`: etapa 3 ou 4 concluída. Campos: `sistema`, `id_externo`, `tentativas`.
- `tentativa_automatica`: nova tentativa agendada após falha técnica. Campos: `etapa`, `numero`, `codigo_http`.
- `erro_detectado`: etapa entra em `erro`. Campos: `etapa`, `tipo` (`tecnico` ou `dado`), `mensagem`.
- `tentativa_manual`: clique em "Tentar novamente". Campos: `etapa`.
- `etapa_manual_concluida`: clique em "Marcar como feito" no Sistema 3. Campos: `minutos_em_espera`.
- `onboarding_concluido`: etapa 6 concluída. Campos: `horas_internas`, `dias_totais`.
- `onboarding_cancelado`: confirmação do cancelamento. Campos: `motivo`, `etapa_no_cancelamento`, `acessos_a_revogar`.

## Fora do MVP

- Navegação e cliques dos usuários internos (sem Google Analytics, sem gravação de sessão).
- Satisfação do cliente com o onboarding (NPS).
- Comparação de desempenho entre pessoas do backoffice.
