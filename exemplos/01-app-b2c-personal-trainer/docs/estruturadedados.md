# Estrutura de dados

*Cinco entidades. Todo `id` é UUID gerado no aparelho, para que um registro criado sem internet já nasça com identidade definitiva. Todo registro tem `criado_em` e `atualizado_em` (timestamp com fuso), usados na sincronização. Datas e horas são gravadas em UTC e exibidas no fuso do personal.*

## Entidade: Personal
O personal trainer dono da conta. Uma conta, uma pessoa.

**Campos:**
- `id` (uuid, único; é o mesmo id do usuário no Supabase Auth)
- `nome` (texto, obrigatório, 2 a 80 caracteres)
- `email` (texto, único, obrigatório)
- `telefone` (texto, opcional, só dígitos com DDD, 10 ou 11)
- `foto_url` (texto, opcional)
- `plano` (enum: `free`, `pro`; obrigatório, padrão `free`)
- `fuso_horario` (texto IANA, obrigatório, padrão `America/Sao_Paulo`)
- `criado_em`, `atualizado_em` (timestamp)

**Relacionamentos:**
- Tem muitos Alunos, HorariosFixos, Agendamentos e Treinos.

---

## Entidade: Aluno
Cada pessoa atendida pelo personal. O aluno não tem login.

**Campos:**
- `id` (uuid, único)
- `personal_id` (uuid, FK para Personal, obrigatório)
- `nome` (texto, obrigatório, 2 a 80 caracteres)
- `telefone` (texto, obrigatório, só dígitos com DDD, 10 ou 11; usado no atalho de WhatsApp)
- `foto_url` (texto, opcional)
- `data_nascimento` (data, opcional)
- `objetivo` (enum: `emagrecimento`, `hipertrofia`, `condicionamento`, `reabilitacao`, `outro`; obrigatório, padrão `condicionamento`)
- `local_padrao` (texto, opcional, até 60 caracteres; ex.: "Smart Fit Paulista")
- `observacoes` (texto, opcional, até 1.000 caracteres; restrições, lesões, preferências)
- `ativo` (booleano, obrigatório, padrão `true`)
- `inativado_em` (timestamp, opcional)
- `criado_em`, `atualizado_em` (timestamp)

**Relacionamentos:**
- Pertence a um Personal.
- Tem muitos HorariosFixos, Agendamentos e Treinos.

---

## Entidade: HorarioFixo
O compromisso semanal recorrente ("Ana, terça às 7h, Smart Fit Paulista"). Um aluno que treina terça e quinta tem dois HorariosFixos.

**Campos:**
- `id` (uuid, único)
- `personal_id` (uuid, FK para Personal, obrigatório)
- `aluno_id` (uuid, FK para Aluno, obrigatório)
- `dia_semana` (inteiro 0 a 6, obrigatório; 0 = domingo)
- `hora_inicio` (hora local, obrigatório; ex.: 07:00)
- `duracao_minutos` (inteiro, obrigatório, padrão 60, entre 15 e 180)
- `local` (texto, opcional, até 60 caracteres; padrão: `local_padrao` do aluno)
- `vigente_desde` (data, obrigatório)
- `vigente_ate` (data, opcional; preenchido quando o horário é encerrado)
- `criado_em`, `atualizado_em` (timestamp)

**Relacionamentos:**
- Pertence a um Personal e a um Aluno.
- Gera muitos Agendamentos.

---

## Entidade: Agendamento
Um treino previsto para uma data e hora. Pode vir de um HorarioFixo ou ser avulso.

**Campos:**
- `id` (uuid, único)
- `personal_id` (uuid, FK para Personal, obrigatório)
- `aluno_id` (uuid, FK para Aluno, obrigatório)
- `horario_fixo_id` (uuid, FK para HorarioFixo, opcional; vazio quando é avulso)
- `inicio` (timestamp, obrigatório)
- `duracao_minutos` (inteiro, obrigatório, padrão 60)
- `local` (texto, opcional, até 60 caracteres)
- `status` (enum: `agendado`, `realizado`, `cancelado`; obrigatório, padrão `agendado`)
- `cancelado_em` (timestamp, opcional)
- `criado_em`, `atualizado_em` (timestamp)

**Relacionamentos:**
- Pertence a um Personal e a um Aluno.
- Pode pertencer a um HorarioFixo.
- Tem no máximo um Treino.

---

## Entidade: Treino
O que de fato aconteceu: o aluno veio ou faltou. É o registro que alimenta histórico e taxa de presença.

**Campos:**
- `id` (uuid, único)
- `personal_id` (uuid, FK para Personal, obrigatório)
- `aluno_id` (uuid, FK para Aluno, obrigatório)
- `agendamento_id` (uuid, FK para Agendamento, opcional, único; vazio quando é treino avulso)
- `data_hora` (timestamp, obrigatório; para treino agendado, copia `inicio` do Agendamento)
- `presenca` (enum: `presente`, `falta`; obrigatório)
- `duracao_minutos` (inteiro, opcional)
- `local` (texto, opcional, até 60 caracteres)
- `observacoes` (texto, opcional, até 500 caracteres)
- `registrado_offline` (booleano, obrigatório, padrão `false`)
- `criado_em`, `atualizado_em` (timestamp)

**Relacionamentos:**
- Pertence a um Personal e a um Aluno.
- Pode pertencer a um Agendamento.

---

## Regras de negócio

### Sobre Personal
- Um personal só enxerga e altera os próprios dados e os de seus alunos. Isso é garantido no banco (RLS), não só na interface.
- No MVP não há limite de alunos: todos ficam no plano `free` sem restrição. O campo `plano` existe para o plano Pro futuro.

### Sobre Aluno
- Aluno inativo some da lista principal, da agenda e dos horários fixos futuros, mas seu histórico continua acessível pelo filtro "Inativos".
- Inativar um aluno encerra os HorariosFixos dele (`vigente_ate` = hoje) e cancela os Agendamentos futuros com status `agendado`.
- Reativar não recria horários: o personal cadastra de novo.
- Aluno não é apagado no MVP, só inativado. Sem foto, a interface mostra as iniciais do nome.

### Sobre HorarioFixo e Agendamento
- O sistema mantém Agendamentos gerados para os próximos 14 dias a partir de cada HorarioFixo vigente. A geração roda ao criar ou editar o horário e uma vez por dia.
- Editar um HorarioFixo afeta só os Agendamentos futuros com status `agendado`; os passados ficam como estão.
- Remarcar um Agendamento muda só aquela ocorrência (`inicio`, `local`); o HorarioFixo não muda.
- Um aluno tem no máximo um Agendamento com status `agendado` por dia. Agendar ou remarcar para um dia ocupado é bloqueado com a mensagem "Ana já tem treino nesse dia".
- Dois alunos diferentes no mesmo horário são permitidos (treino em dupla), sem aviso.
- Agendamento `cancelado` não vira Treino e não conta na taxa de presença.
- Agendamento com início no passado e ainda `agendado` aparece como "sem registro" na agenda daquele dia, até ser registrado ou cancelado. Nunca é convertido em Treino automaticamente.

### Sobre Treino
- Treino só pode ter `data_hora` igual ou anterior a agora. Treino futuro é Agendamento.
- Registrar presença ou falta de um Agendamento cria o Treino e muda o Agendamento para `realizado`, na mesma operação.
- Um Agendamento tem no máximo um Treino. Registrar de novo edita o Treino existente.
- Desfazer um registro (até 6 segundos depois, pelo aviso na tela) apaga o Treino e devolve o Agendamento para `agendado`.
- Treino pode ser editado (presença e observação) a qualquer momento; não pode ser apagado depois do prazo de desfazer.
- Taxa de presença do aluno = treinos `presente` / (treinos `presente` + treinos `falta`) nos últimos 90 dias. Sem treinos, mostra "sem dados".

### Sobre sincronização
- Em conflito entre duas versões do mesmo registro, vence a de `atualizado_em` mais recente (última edição ganha). Sem merge campo a campo no MVP.

---

*A IA deve usar essa estrutura para criar o banco de dados, validações e relacionamentos. Pense nisso como um diagrama ER em texto.*
