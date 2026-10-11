# Fluxos e telas

*Aqui fica o que existe no produto e por onde a pessoa anda. Cor, fonte e estilo ficam no DESIGN.md.*

## Princípios de experiência
1. **Uma mão, polegar direito.** Toda ação frequente fica na metade de baixo da tela. Nada importante no canto superior esquerdo.
2. **Registrar presença em um toque.** A ação mais frequente do produto custa um toque a partir da agenda. Qualquer outra ação frequente custa no máximo dois.
3. **Visão geral primeiro, detalhe sob demanda.** Agenda e lista mostram o mínimo para decidir; o resto fica no perfil do aluno.
4. **Funciona sem internet.** Nenhuma tela do dia a dia espera a rede para mostrar ou salvar. A sincronização é invisível até falhar.
5. **Feedback na hora, e reversível.** Toda ação mostra o resultado em menos de 300 ms e as destrutivas oferecem "Desfazer" em vez de pedir confirmação.

## Mapa de telas
- **Boas-vindas**: escolher entre criar conta e entrar.
- **Criar conta**: cadastro do personal em um formulário curto.
- **Entrar**: login com e-mail e senha.
- **Recuperar senha**: pedir o link de redefinição por e-mail e, ao abrir o link, definir a nova senha.
- **Agenda** (aba "Hoje", tela inicial): ver os treinos do dia e registrar presença.
- **Alunos** (aba): encontrar um aluno, ver quem está sumido, cadastrar novo.
- **Perfil do aluno**: histórico, observações, horários fixos e ações sobre o aluno.
- **Formulário de aluno**: cadastrar ou editar aluno.
- **Menu Adicionar** (folha inferior): atalhos para novo aluno, treino avulso e agendamento.
- **Registrar treino** (folha inferior): presença ou falta com observação, remarcar ou cancelar.
- **Agendar treino** (folha inferior): agendamento avulso ou horário fixo semanal.
- **Minha conta**: dados do personal, sair, suporte.

A navegação principal é uma barra inferior com três itens: "Hoje", botão central "+" (abre o Menu Adicionar) e "Alunos". Minha conta abre pela foto do personal no cabeçalho da Agenda.

---

## Tela: Boas-vindas

**Objetivo:** entrar no app em um toque, sem tour.

### Hierarquia do conteúdo
1. Nome do produto e uma frase: "Sua agenda e seus alunos, no bolso."
2. Botão principal "Criar conta".
3. Botão secundário "Já tenho conta".

### Ações e interações
- "Criar conta" → Criar conta.
- "Já tenho conta" → Entrar.
- Se já existe sessão válida, esta tela não aparece: o app abre direto na Agenda.

---

## Tela: Criar conta

**Objetivo:** criar a conta em menos de 1 minuto.

### Hierarquia do conteúdo
1. Campos: nome, e-mail, senha (mínimo 8 caracteres, com botão de mostrar).
2. Botão "Criar conta".
3. Link "Já tenho conta".
4. Texto curto com link para termos e privacidade.

### Ações e interações
- "Criar conta" → valida, cria a conta e abre a Agenda vazia. Não pede confirmação de e-mail antes de entrar.
- E-mail já cadastrado → mensagem no campo: "Esse e-mail já tem conta. Quer entrar?" com link para Entrar.
- Teclado abre no tipo certo para cada campo (e-mail, senha) e "Avançar" pula para o próximo campo.

---

## Tela: Entrar

**Objetivo:** voltar ao app quando a sessão acabou ou trocou de celular.

### Hierarquia do conteúdo
1. Campos: e-mail e senha.
2. Botão "Entrar".
3. Link "Esqueci a senha".

### Ações e interações
- "Entrar" → abre a Agenda. A sessão dura 60 dias sem pedir login de novo.
- Credenciais erradas → mensagem abaixo do botão: "E-mail ou senha não conferem." Sem dizer qual dos dois.
- "Esqueci a senha" → Recuperar senha, com o e-mail já preenchido.

---

## Tela: Recuperar senha

**Objetivo:** receber o link de redefinição.

### Hierarquia do conteúdo
1. Campo de e-mail.
2. Botão "Enviar link".
3. Depois de enviar: "Se esse e-mail tiver conta, o link chega em alguns minutos. Confira o spam."

### Ações e interações
- "Enviar link" → dispara o e-mail e mostra a mensagem acima, sempre a mesma, exista a conta ou não.
- O link abre o app numa tela simples de nova senha e, ao salvar, entra na Agenda.

---

## Tela: Agenda (aba "Hoje")

**Objetivo:** abrir o app e saber, em 2 segundos, quem treina agora e quem falta registrar.

### Hierarquia do conteúdo
1. **Cabeçalho:** foto do personal (abre Minha conta) e a data por extenso ("Terça, 14 de outubro").
2. **Faixa de dias:** 7 dias a partir de hoje (dia da semana e número), com o dia escolhido destacado. Rola para a direita até 14 dias e para a esquerda até 7 dias atrás.
3. **Resumo do dia:** "6 treinos · 2 registrados".
4. **Seção "Sem registro"** (só aparece se houver): agendamentos de dias anteriores, até 7 dias atrás, que ficaram sem presença ou falta.
5. **Lista do dia**, em ordem de horário. Cada card tem:
   - horário de início, em destaque;
   - foto ou iniciais do aluno;
   - nome do aluno;
   - local, em texto secundário;
   - botão "Presente" à direita, ao alcance do polegar.
6. Cards já registrados descem para o fim da lista, com o selo "Presente" ou "Faltou" no lugar do botão. Cancelados ficam no fim, com o selo "Cancelado".

### Ações e interações
- Toque em "Presente" → registra presença na hora, o card ganha o selo "Presente" e desce, e aparece um aviso na base da tela por 6 segundos: "Treino da Ana registrado" com as ações "Observação" e "Desfazer".
- "Observação" no aviso → abre Registrar treino com o campo de observação já focado.
- Toque no card (fora do botão) → abre Registrar treino, que também mostra a última observação do aluno. É o caminho para relembrar o aluno antes do treino.
- Deslizar o card para a esquerda → mostra "Remarcar" e "Cancelar". As mesmas ações existem dentro de Registrar treino, para quem não descobre o gesto.
- Toque num dia da faixa → troca a lista para aquele dia. Em dias futuros o botão "Presente" não aparece (regra: treino futuro é agendamento).
- Puxar para baixo → força sincronização.
- Toque no "+" central → Menu Adicionar.

---

## Tela: Alunos (aba)

**Objetivo:** achar um aluno em menos de 5 segundos e ver quem está sumido.

### Hierarquia do conteúdo
1. Título "Alunos" e contador ("15 ativos").
2. Campo de busca, fixo no topo da lista.
3. Filtros em pílula: "Ativos" (padrão), "Sumidos", "Inativos".
4. Lista de alunos. Cada linha tem:
   - foto ou iniciais;
   - nome;
   - próximo treino ("Amanhã, 7h") ou "Sem treino marcado";
   - último treino ("Há 2 dias");
   - selo "Sumido" se o último treino `presente` foi há mais de 10 dias.
5. Ordem padrão: próximo treino mais perto primeiro; quem não tem treino marcado vai para o fim, em ordem alfabética.

### Ações e interações
- Busca → filtra por nome enquanto digita, sem diferenciar acento e maiúscula.
- Toque no aluno → Perfil do aluno.
- Deslizar para a esquerda → "Editar" e "Inativar". Inativar mostra o aviso com "Desfazer".
- Filtro "Sumidos" → só alunos ativos com o selo "Sumido", do mais antigo para o mais recente.

---

## Tela: Perfil do aluno

**Objetivo:** em 10 segundos, lembrar quem é o aluno e o que aconteceu no último treino.

### Hierarquia do conteúdo
1. **Topo:** voltar, foto, nome, objetivo e ação "Editar".
2. **Atalhos:** "WhatsApp" e "Ligar", lado a lado.
3. **Última observação:** texto e data do treino mais recente que tem observação. Se não houver, a seção não aparece.
4. **Números rápidos:** treinos no mês atual, taxa de presença nos últimos 90 dias, data do último treino.
5. **Observações gerais** do aluno (restrições, lesões, preferências).
6. **Horários fixos:** lista ("Terça, 7h, Smart Fit Paulista") com ação "Adicionar horário".
7. **Histórico:** treinos do mais recente para o mais antigo, 10 por vez, cada um com data, selo (Presente, Faltou, Cancelado) e observação em até duas linhas.
8. **Ações na base:** botão principal "Agendar treino" e botão secundário "Registrar treino avulso".

### Ações e interações
- "WhatsApp" → abre conversa com o telefone do aluno, sem mensagem pronta.
- "Ligar" → abre o discador.
- Toque num treino do histórico → expande a observação inteira, com "Editar" (abre Registrar treino daquele treino).
- "Ver mais" no fim do histórico → carrega mais 10.
- Toque num horário fixo → abre Agendar treino em modo de edição do horário, com "Encerrar horário" no fim.
- "Agendar treino" → Agendar treino com o aluno preenchido.
- "Registrar treino avulso" → Registrar treino com aluno preenchido e data e hora de agora.
- Aluno inativo: o topo mostra o selo "Inativo", as ações da base somem e aparece "Reativar aluno".

---

## Tela: Formulário de aluno

**Objetivo:** cadastrar um aluno em menos de 40 segundos, com só dois campos obrigatórios.

### Hierarquia do conteúdo
1. Foto (opcional): tirar agora ou escolher da galeria.
2. Nome (obrigatório).
3. Telefone com DDD (obrigatório), com máscara e opção "Importar dos contatos".
4. Objetivo em pílulas: Emagrecimento, Hipertrofia, Condicionamento, Reabilitação, Outro.
5. Local de treino padrão, com sugestões dos locais já usados pelo personal.
6. Observações gerais.
7. Data de nascimento, recolhida em "Mais detalhes".
8. Botão "Salvar aluno" fixo na base.
9. Só na edição: "Inativar aluno", em texto, no fim do formulário.

### Ações e interações
- "Importar dos contatos" → pede permissão de contatos uma vez e preenche nome e telefone.
- "Salvar aluno" com campo inválido → rola até o primeiro erro e mostra a mensagem abaixo do campo.
- "Salvar aluno" no cadastro → salva e pergunta numa folha: "Quer marcar o horário fixo da Ana?" com "Marcar horário" (abre Agendar treino com "Toda semana" ligado) e "Agora não" (vai para o Perfil do aluno).
- Na edição, "Salvar" volta para o Perfil do aluno. Sair com alteração não salva pede confirmação.

---

## Tela: Menu Adicionar (folha inferior)

**Objetivo:** começar qualquer cadastro com o polegar.

### Hierarquia do conteúdo
1. "Registrar treino avulso".
2. "Agendar treino".
3. "Novo aluno".

### Ações e interações
- Cada opção abre a tela correspondente. "Registrar treino avulso" e "Agendar treino" começam pelo seletor de aluno (busca com os 5 alunos mais recentes no topo).
- Arrastar para baixo ou tocar fora fecha.

---

## Tela: Registrar treino (folha inferior)

**Objetivo:** registrar presença ou falta com observação, ou resolver um treino que não vai acontecer.

### Hierarquia do conteúdo
1. Aluno, data e horário (e local, se houver).
2. Última observação do aluno, em até 3 linhas, com a data, e o link "Ver perfil". Some quando o aluno não tem observação.
3. Escolha principal, dois botões grandes: "Presente" e "Faltou".
4. Campo "Observação" (até 500 caracteres, com contador a partir de 400).
5. Botão "Salvar".
6. Ações secundárias, só quando o treino veio de um agendamento ainda não registrado: "Remarcar" e "Cancelar treino".

### Ações e interações
- Abre com "Presente" pré-selecionado quando o horário já passou; sem seleção quando ainda não chegou a hora.
- "Salvar" → grava, fecha a folha e mostra o aviso com "Desfazer". Sem "Presente" ou "Faltou" escolhido, o botão fica desabilitado.
- "Ver perfil" → fecha a folha e abre o Perfil do aluno.
- "Remarcar" → abre Agendar treino só com data, hora e local daquela ocorrência.
- "Cancelar treino" → cancela o agendamento, fecha a folha e mostra "Treino cancelado" com "Desfazer".
- No treino avulso, o topo vira seletor de aluno e campo de data e hora (padrão: agora; não aceita futuro).

---

## Tela: Agendar treino (folha inferior)

**Objetivo:** marcar um treino avulso ou um horário fixo semanal em até 4 toques.

### Hierarquia do conteúdo
1. Aluno (preenchido quando vem do perfil).
2. Data (padrão: amanhã) e hora (padrão: o horário fixo mais comum do aluno, ou 7h).
3. Chave "Repetir toda semana". Ligada, a data vira escolha de dia da semana e o resultado é um horário fixo.
4. Duração (padrão 60 min) e local (padrão: local do aluno).
5. Botão "Agendar" (ou "Salvar horário fixo" com a chave ligada).
6. No modo edição de horário fixo: "Encerrar horário", no fim.

### Ações e interações
- "Agendar" → cria o agendamento, fecha a folha e mostra "Treino marcado para quinta, 7h".
- Com a chave ligada → cria o horário fixo e os agendamentos dos próximos 14 dias.
- Dia ocupado para aquele aluno → bloqueia com "Ana já tem treino nesse dia" e mantém a folha aberta.
- "Encerrar horário" → para de gerar novos agendamentos e cancela os futuros daquele horário, com "Desfazer".

---

## Tela: Minha conta

**Objetivo:** ajustar o básico e sair.

### Hierarquia do conteúdo
1. Foto, nome e e-mail do personal, com "Editar".
2. Fuso horário (padrão São Paulo).
3. "Falar com o suporte" (abre WhatsApp do suporte).
4. "Sair".
5. Versão do app e status da última sincronização ("Tudo salvo às 14:32" ou "3 registros esperando internet").

### Ações e interações
- "Sair" com registros esperando internet → avisa "Você tem 3 registros que ainda não subiram. Se sair agora, eles se perdem." com "Esperar" e "Sair mesmo assim".
- "Sair" sem pendências → volta para Boas-vindas.

---

## Fluxo principal: registrar presença pela agenda (Carlos)
1. Carlos termina o treino das 7h e abre o app. A Agenda abre direto em "Hoje", a partir do cache, sem esperar a rede.
2. O card da Ana (7h) está no topo dos não registrados.
3. Toca em "Presente".
4. O card ganha o selo e desce. O aviso "Treino da Ana registrado" aparece com "Observação" e "Desfazer".
5. Se quiser, toca em "Observação", dita pelo microfone do teclado e toca em "Salvar".

**Tempo esperado:** até 10 segundos sem observação, até 30 segundos com observação ditada.

## Fluxo: registrar falta ou presença com observação
1. Na Agenda, toca no card do aluno.
2. Registrar treino abre com "Presente" pré-selecionado. Toca em "Faltou", se for o caso.
3. Escreve ou dita a observação.
4. Toca em "Salvar". Aviso com "Desfazer".

**Tempo esperado:** até 20 segundos.

## Fluxo: consultar o aluno antes do treino (Carlos)
1. Na Agenda, toca no card do próximo aluno. Como o horário ainda não chegou, Registrar treino abre sem nada selecionado.
2. Lê a última observação no topo da folha.
3. Se precisar de mais, toca em "Ver perfil" e lê os números rápidos e o histórico.
4. Arrasta a folha para baixo e volta para a Agenda.

**Tempo esperado:** até 15 segundos. Funciona sem internet para os últimos 30 treinos do aluno.

## Fluxo: montar a semana (Juliana)
1. Domingo à noite, abre a Agenda e percorre a faixa de dias de segunda a sábado.
2. Num treino que o aluno avisou que não vai, desliza o card e toca em "Cancelar".
3. Para uma reposição, desliza outro card e toca em "Remarcar", escolhendo novo dia e hora.
4. Para um aluno novo de horário fixo, toca no "+", "Agendar treino", escolhe o aluno, liga "Repetir toda semana", escolhe terça e quinta às 18h (um horário fixo por dia) e salva.
5. Na aba Alunos, abre o filtro "Sumidos" para decidir com quem falar na semana e toca em "WhatsApp" no perfil.

**Tempo esperado:** até 10 minutos para 20 alunos, contra cerca de 2 horas na planilha.

## Fluxo: primeiro acesso
1. Boas-vindas → "Criar conta" → nome, e-mail e senha → "Criar conta".
2. Abre a Agenda vazia, com o convite "Cadastre seu primeiro aluno" e o botão "Cadastrar aluno". Não há tour nem tutorial.
3. Formulário de aluno: nome e telefone (ou "Importar dos contatos") → "Salvar aluno".
4. "Quer marcar o horário fixo da Ana?" → "Marcar horário" → escolhe dias e hora → "Salvar horário fixo".
5. Volta para a Agenda, já com os treinos dos próximos dias. O convite vira "Cadastre mais alunos para ver a semana completa" até o terceiro aluno.

**Tempo esperado:** até 3 minutos do download ao primeiro aluno com horário fixo.

## Fluxo: treino avulso
1. Toca no "+" → "Registrar treino avulso".
2. Escolhe o aluno (busca ou recentes).
3. Data e hora já vêm como agora. Escolhe "Presente" ou "Faltou" e, se quiser, a observação.
4. "Salvar". O treino entra no histórico do aluno e não cria agendamento.

**Tempo esperado:** até 20 segundos.

## Fluxo: inativar e reativar aluno
1. Na aba Alunos, desliza o aluno e toca em "Inativar" (ou, no perfil, "Editar" e depois "Inativar aluno" no fim do formulário).
2. O aluno sai da lista, os horários fixos são encerrados e os treinos futuros cancelados. Aviso com "Desfazer" por 6 segundos.
3. Para reativar: filtro "Inativos" → perfil → "Reativar aluno". O personal marca os horários de novo.

## Fluxo: usar sem internet
1. O sinal cai. Aparece uma faixa fina no topo: "Sem internet. Seus registros ficam salvos no celular."
2. Carlos registra presença, escreve observação, cadastra aluno e agenda treino normalmente. Cada item fica numa fila local.
3. A internet volta. A fila sobe sozinha, na ordem em que foi criada. A faixa troca para "Tudo salvo" por 3 segundos e some.
4. Se algum item falhar ao subir (ex.: conflito com o dia ocupado), o card mostra o selo "Não salvo" e, ao tocar, a explicação e as opções "Tentar de novo" ou "Descartar".

---

## Estados

### Vazio
- **Agenda, sem nenhum aluno:** ilustração simples, "Cadastre seu primeiro aluno" e botão "Cadastrar aluno".
- **Agenda, dia sem treinos:** "Nenhum treino marcado para terça." com "Agendar treino" e "Registrar treino avulso".
- **Alunos, busca sem resultado:** "Nenhum aluno com 'Mar'." com "Cadastrar Mar" (abre o formulário com o nome preenchido).
- **Alunos, filtro Sumidos vazio:** "Ninguém sumido. Todo mundo treinou nos últimos 10 dias."
- **Perfil, sem histórico:** "Nenhum treino registrado ainda." e o botão "Agendar treino" em destaque.
- **Perfil, sem horário fixo:** "Sem horário fixo." com "Adicionar horário".

### Carregando
- A Agenda e a lista de Alunos abrem sempre do cache local; nunca mostram tela de carregamento cheia.
- Primeiro acesso em celular novo (cache vazio): esqueleto dos cards por até 3 segundos. Passou disso, mostra "Ainda carregando, a internet está lenta." sem bloquear a tela.
- Foto que não carregou: iniciais no lugar, sem ícone de erro.
- "Ver mais" no histórico mostra 3 linhas de esqueleto no fim da lista.

### Erro
- **Validação:** mensagem abaixo do campo, em linguagem de gente ("Coloque o telefone com DDD, ex.: 11 98765-4321"). Nunca em janela.
- **Falha ao subir um registro:** selo "Não salvo" no item, com "Tentar de novo" e "Descartar". O dado nunca some sem o personal decidir.
- **Erro inesperado numa tela:** "Algo deu errado aqui. Seus registros estão salvos." com "Tentar de novo". O erro vai para o monitoramento.
- **Sessão expirada no servidor:** os dados locais continuam visíveis; ao tentar sincronizar, pede para entrar de novo e, depois do login, sobe a fila.

### Sem conexão
- Faixa fina no topo de todas as telas, com o texto acima. Não bloqueia nada.
- Funciona offline: Agenda dos 7 dias anteriores e dos 14 seguintes, alunos ativos, últimos 30 treinos de cada aluno, todos os registros e cadastros.
- Não funciona offline: criar conta, entrar, recuperar senha, ver histórico além dos 30 treinos em cache (mostra "Conecte-se para ver treinos mais antigos").
- Foto tirada offline fica no celular e sobe junto com a fila.

### Sem permissão
- **Câmera ou galeria negada:** o campo de foto mostra "Sem acesso à câmera. Libere nos ajustes do celular." com atalho para os ajustes. O cadastro segue sem foto.
- **Contatos negado:** "Importar dos contatos" some e o telefone fica para digitar.
- **Registro de outro personal:** não existe na interface; o banco bloqueia (RLS). Se acontecer, trata como erro inesperado.

---

*A IA deve usar essas descrições para criar as telas. A hierarquia, os textos de interface citados e os tempos esperados devem ser respeitados. Visual, espaçamento e componentes vêm do DESIGN.md.*
