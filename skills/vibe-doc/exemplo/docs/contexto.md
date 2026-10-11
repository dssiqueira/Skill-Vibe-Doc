# Contexto do produto

## Problema
Personal trainer independente, com 10 a 30 alunos, controla agenda, presença e observações espalhadas entre WhatsApp, caderno e planilha. Na prática:
- não lembra quando foi o último treino de cada aluno nem o que anotou da última vez, e o aluno percebe;
- perde de 1 a 2 horas por semana reorganizando planilha e conferindo quem veio;
- esquece de cobrar porque não sabe quantos treinos cada aluno fez no mês;
- perde aluno por desorganização (horário trocado, treino esquecido).

## Solução
Um app de celular que o personal abre entre um atendimento e outro. Situação real: Carlos termina o treino das 7h com a Ana no vestiário da academia, abre o Treinou, toca em "Presente" no card da Ana e, se quiser, dita uma observação ("reclamou do joelho esquerdo no agachamento"). Leva menos de 10 segundos. Às 8h, enquanto o próximo aluno não chega, abre o perfil dele e lê o que anotou na semana passada.

## Audiência principal
Personal trainer autônomo, que trabalha sozinho, com 10 a 30 alunos ativos, atendendo em academia, parque ou na casa do aluno. O celular (quase sempre Android) é a única ferramenta de trabalho. Usa o app com uma mão, em pé, com 5 a 10 minutos de intervalo e sinal de internet instável.

## Escopo do MVP
Na ordem em que deve ser construído:
1. Cadastro e login do personal (e-mail e senha).
2. Cadastro de alunos com foto, telefone, objetivo e observações gerais.
3. Agenda por dia, com horários fixos semanais (ex.: Ana, terça e quinta às 7h) e agendamentos avulsos.
4. Registro de presença ou falta em um toque, com observação opcional.
5. Perfil do aluno com histórico de treinos, observações e taxa de presença.
6. Funcionamento sem internet para agenda, registro de presença e consulta de histórico recente.

## O que NÃO é (pelo menos agora)
- Não é app para o aluno. O aluno não tem login, não confirma presença e não recebe nada do app.
- Não monta ficha de treino (exercícios, séries, cargas) nem tem biblioteca de vídeos.
- Não cobra nem recebe pagamento de aluno. Controle financeiro e cobrança ficam para depois da validação.
- Não faz avaliação física, nutrição ou dieta.
- Não é rede social nem vitrine para captar alunos.
- Não é sistema para academia ou estúdio com vários profissionais: uma conta é um personal.

## Critério de sucesso
No beta fechado com 30 personais recrutados, ao fim de 8 semanas:
- pelo menos 18 personais (60%) registram 10 treinos ou mais por semana, em 4 semanas seguidas;
- a mediana do tempo para registrar presença a partir da agenda fica abaixo de 10 segundos;
- 70% dos personais registram o primeiro treino em até 24 horas após o cadastro.

## Critério de morte
Se, na semana 6 do beta, menos de 9 dos 30 personais (30%) continuarem registrando pelo menos 5 treinos por semana, paramos de construir funcionalidade nova, entrevistamos quem abandonou e decidimos entre pivotar (ex.: foco em cobrança em vez de agenda) ou encerrar. Esse número foi definido antes da primeira linha de código e não é renegociado durante o beta.

---
*Este arquivo deve ser lido pela IA antes de qualquer implementação. Ele define o produto, não a solução técnica.*
