# Métricas

*As métricas de negócio respondem ao critério de sucesso e ao critério de morte do `contexto.md`. Se uma métrica não ajuda a decidir nada, ela não entra.*

## Métricas de negócio

### Personais ativos de verdade
**O que medir:** quantos personais registram pelo menos 10 treinos (presença ou falta) numa semana.
**Por que importa:** é a régua do critério de sucesso. Abrir o app não conta; registrar treino conta.
**Como calcular:** personais distintos com 10 ou mais eventos `treino_registrado` na semana (segunda a domingo, fuso do personal), menos os desfeitos (`treino_desfeito`).
**Meta:** 18 de 30 (60%) por 4 semanas seguidas até a semana 8 do beta.
**Alerta de morte:** menos de 9 de 30 (30%) com 5 ou mais treinos registrados na semana 6.

### Retenção semanal de personais
**O que medir:** dos personais que registraram treino na semana 1 após o cadastro, quantos registram na semana 4 e na semana 8.
**Por que importa:** mostra se o app virou hábito ou foi testado e largado.
**Como calcular:** coorte por semana de `personal_cadastrado`; ativo na semana N = pelo menos 1 `treino_registrado` na semana N.
**Meta:** 70% na semana 4 e 60% na semana 8.

### Tempo até o primeiro treino registrado
**O que medir:** tempo entre o cadastro e o primeiro treino registrado.
**Por que importa:** mostra se o primeiro acesso funciona sem tutorial.
**Como calcular:** `timestamp` do primeiro `treino_registrado` menos o de `personal_cadastrado`, por personal.
**Meta:** 70% em até 24 horas.

### Dias de uso por semana
**O que medir:** em quantos dias da semana o personal registra ou consulta algo.
**Por que importa:** personal atende quase todo dia; menos de 4 dias de uso indica que parte da rotina continua no caderno.
**Como calcular:** dias distintos com `agenda_visualizada` ou `treino_registrado`, média dos últimos 28 dias.
**Meta:** 4 dias ou mais por semana.

## Métricas de uso

### Tempo para registrar presença
**O que medir:** segundos entre a Agenda aparecer na tela e o toque que registrou o treino.
**Por que importa:** é a promessa central do produto (menos de 10 segundos) e a primeira coisa que o Carlos sente.
**Registrar:** campo `segundos_desde_abertura` no evento `treino_registrado`.
**Meta:** mediana abaixo de 10 segundos para `origem = agenda_botao`.

### Treinos registrados por personal por semana
**O que medir:** volume de registros por personal, separado por origem.
**Por que importa:** compara com o número de agendamentos; se o personal tem 40 treinos marcados e registra 10, o resto está indo para o caderno.
**Registrar:** evento `treino_registrado` com `origem` e `presenca`.

### Cobertura de registro
**O que medir:** percentual de agendamentos da semana que terminam registrados (presente ou falta) ou cancelados, em vez de ficar "sem registro".
**Por que importa:** agenda com muito "sem registro" vira lixo e o personal para de confiar nela.
**Como calcular:** (agendamentos `realizado` + `cancelado`) / agendamentos com início na semana, consultado direto no banco.
**Meta:** 85% ou mais.

### Uso offline
**O que medir:** percentual de treinos registrados sem internet e quanto tempo a fila ficou parada.
**Por que importa:** confirma (ou derruba) a decisão de investir em offline.
**Registrar:** campo `offline` em `treino_registrado` e evento `sincronizacao_concluida`.

### Uso de observação
**O que medir:** percentual de treinos registrados com observação.
**Por que importa:** observação é o que faz o aluno sentir que o personal lembra dele; se ninguém usa, o atalho no aviso precisa mudar.
**Registrar:** campo `com_observacao` em `treino_registrado` e evento `treino_editado`.

## Eventos a registrar

Todo evento leva automaticamente `personal_id`, `timestamp`, `plataforma` (android, ios), `versao_app` e `offline` (booleano). Nenhum evento leva nome, telefone ou texto de observação do aluno.

### Conta
- `personal_cadastrado`: tocou em "Criar conta" e a conta foi criada.
- `login_realizado`: entrou pela tela Entrar.
- `senha_recuperacao_solicitada`: tocou em "Enviar link" em Recuperar senha.
- `logout_realizado`: tocou em "Sair" em Minha conta. Campos: `itens_pendentes`.

### Agenda e treinos
- `agenda_visualizada`: a Agenda ganhou foco (abertura do app, volta para a aba ou troca de dia). Campos: `data_exibida`, `qtd_agendamentos`, `qtd_sem_registro`.
- `treino_registrado`: presença ou falta gravada. Campos: `treino_id`, `aluno_id`, `presenca` (presente, falta), `origem` (agenda_botao, agenda_folha, avulso), `com_observacao`, `segundos_desde_abertura`.
- `treino_desfeito`: tocou em "Desfazer" no aviso após registrar. Campos: `treino_id`.
- `treino_editado`: salvou mudança num treino já registrado, inclusive a observação adicionada pelo aviso. Campos: `treino_id`, `campo_alterado` (presenca, observacoes).

### Agendamentos e horários fixos
- `agendamento_criado`: tocou em "Agendar" com a chave "Repetir toda semana" desligada. Campos: `agendamento_id`, `aluno_id`, `dias_ate_treino`.
- `agendamento_remarcado`: salvou nova data ou hora em "Remarcar". Campos: `agendamento_id`, `dias_deslocados`.
- `agendamento_cancelado`: tocou em "Cancelar" ou "Cancelar treino". Campos: `agendamento_id`, `horas_antes_do_inicio`.
- `horario_fixo_criado`: salvou com "Repetir toda semana" ligada. Campos: `horario_fixo_id`, `aluno_id`, `dia_semana`.
- `horario_fixo_editado`: salvou mudança num horário fixo existente. Campos: `horario_fixo_id`.
- `horario_fixo_encerrado`: tocou em "Encerrar horário". Campos: `horario_fixo_id`, `agendamentos_cancelados`.

### Alunos
- `aluno_cadastrado`: tocou em "Salvar aluno" num cadastro novo. Campos: `aluno_id`, `com_foto`, `importado_contatos`, `objetivo`.
- `aluno_editado`: salvou edição do aluno. Campos: `aluno_id`.
- `aluno_inativado`: tocou em "Inativar" (e não desfez). Campos: `aluno_id`, `dias_desde_cadastro`.
- `aluno_reativado`: tocou em "Reativar aluno". Campos: `aluno_id`.
- `aluno_visualizado`: abriu o Perfil do aluno. Campos: `aluno_id`, `origem` (agenda, lista, busca).
- `historico_expandido`: tocou em "Ver mais" no histórico. Campos: `aluno_id`, `pagina`.
- `whatsapp_aberto`: tocou em "WhatsApp" no perfil. Campos: `aluno_id`, `aluno_sumido` (booleano).

### Sincronização
- `sincronizacao_concluida`: a fila local subiu depois de um período sem internet. Campos: `itens_enviados`, `itens_com_erro`, `segundos_offline`.

## Fora do MVP
- Painel de métricas dentro do app para o personal. Os números rápidos do Perfil do aluno bastam.
- Dashboard interno sofisticado: no beta, as consultas acima rodam no PostHog e no SQL do Supabase.
- Mapa de calor, gravação de sessão e funil por tela.
- Receita, cobrança e qualquer métrica financeira (não há pagamento no MVP).
- Latência e taxa de erro de API ficam no monitoramento técnico (`integracoes.md`), não aqui.

---

*A IA deve implementar esses eventos junto com a ação que os dispara, na mesma entrega. Não criar tela de analytics no MVP.*
