# Decisões técnicas

*A mais recente em cima. Antes de reabrir uma decisão, traga um motivo que não estava aqui.*

---

## 2026-03-18 Sem IA no MVP, inclusive para resumir observações

- **Contexto:** surgiu a ideia de gerar, com um modelo de linguagem, um resumo das últimas observações do aluno no topo do perfil ("joelho esquerdo dolorido há 3 semanas, evoluiu no supino").
- **Decisão:** nada de IA no MVP. O perfil mostra a última observação inteira e o histórico em ordem.
- **Alternativas descartadas:** resumo por LLM ao abrir o perfil (depende de internet, que falta justamente no vestiário; acrescenta 1 a 3 segundos num fluxo que precisa de 10; custo por chamada sem receita no beta; risco de inventar uma lesão que o aluno não tem, num contexto de saúde). Transcrição própria de áudio (o microfone do teclado do celular já faz isso de graça).
- **Nível de autonomia:** sem IA. A observação mais recente resolve a dor do Carlos ("lembrar o que anotei semana passada") e o degrau mais baixo bastou. Reavaliar quando houver alunos com mais de 50 treinos registrados e o beta mostrar que o personal rola o histórico com frequência (`historico_expandido`).
- **Onde entra o humano:** o personal escreve e lê todas as observações; nada é gerado por máquina.

## 2026-03-16 Horário fixo vira agendamentos reais para 14 dias

- **Contexto:** quase todo aluno de personal treina em horário fixo (ex.: terça e quinta às 7h), e a agenda precisa permitir cancelar ou remarcar uma única ocorrência, inclusive sem internet.
- **Decisão:** entidade `HorarioFixo` separada, que gera registros de `Agendamento` para os próximos 14 dias (função SQL ao salvar e `pg_cron` diário).
- **Alternativas descartadas:** regra de recorrência calculada na tela, tipo RRULE (cancelar uma ocorrência exige tabela de exceções e a lógica teria de existir igual no app offline e no servidor). Campo `recorrente` dentro do próprio agendamento, como no rascunho inicial (não separa "o combinado" de "o que vai acontecer na quinta", e editar o horário quebraria o passado).
- **Onde entra o humano:** o personal decide quando encerrar um horário; o sistema nunca encerra sozinho, nem para aluno sumido.

## 2026-03-12 Offline com fila local e última edição ganha

- **Contexto:** o Carlos registra presença em vestiário e subsolo de academia, com sinal fraco ou nenhum, e a persona Juliana desiste de app que não funciona no parque.
- **Decisão:** cache de leitura persistido (TanStack Query com MMKV) e fila local de mutações com UUID gerado no aparelho. Conflito resolvido por `atualizado_em`: última edição ganha.
- **Alternativas descartadas:** só online com mensagem de erro (quebra o fluxo principal no lugar onde ele mais acontece). Banco local completo com sincronização bidirecional, como WatermelonDB ou PowerSync (resolve conflitos melhor, mas dobra o esquema e a complexidade para um caso, um personal editando o mesmo treino em dois aparelhos, que quase não existe). Merge campo a campo (mesmo motivo).
- **Onde entra o humano:** quando um item falha ao subir, o personal decide entre tentar de novo e descartar; o app nunca descarta sozinho.

## 2026-03-10 Supabase como banco, autenticação e arquivos

- **Contexto:** o produto precisa de login, banco relacional com isolamento por personal e armazenamento de fotos, construído por uma pessoa só com ajuda de IA.
- **Decisão:** Supabase (Postgres, Auth e Storage) na região de São Paulo, com Row Level Security em todas as tabelas.
- **Alternativas descartadas:** Firebase (Firestore é documento, e as regras do produto são relacionais: um agendamento por aluno por dia, um treino por agendamento, taxa de presença por período; tudo isso fica mais simples e seguro como restrição SQL). Backend próprio com Next.js e Postgres (mais código para manter, sem ganho no MVP).
- **Onde entra o humano:** toda migration passa por revisão antes de rodar em `staging` e `prod`.

## 2026-03-08 App nativo com Expo em vez de PWA

- **Contexto:** a persona principal usa Android intermediário, com uma mão, offline com frequência, e precisa de câmera, contatos e abertura instantânea.
- **Decisão:** Expo (React Native) com TypeScript e Expo Router, distribuído pela Google Play primeiro e pela App Store depois.
- **Alternativas descartadas:** PWA com Next.js (instalação confusa para o Carlos, armazenamento offline que o iOS pode apagar, sem acesso a contatos, ícone que some da tela inicial). Flutter (a stack de apoio, como Supabase, PostHog e Sentry, e a IA de código rendem mais em TypeScript; uma linguagem só no app e nas funções).
- **Onde entra o humano:** publicação nas lojas e cada envio para `prod` são aprovados manualmente.
