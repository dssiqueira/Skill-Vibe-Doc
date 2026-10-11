# Treinou

App de celular para personal trainer autônomo gerenciar agenda, presença e histórico dos alunos entre um atendimento e outro. A promessa: registrar presença em um toque, em menos de 10 segundos, mesmo sem internet.

## Antes de mexer em qualquer coisa

Leia, nesta ordem:

1. `docs/contexto.md`: problema, público, escopo, o que não é, critério de sucesso e de morte.
2. `docs/personas.md`: Carlos (principal, Android, uma mão, sem sinal) e Juliana. Em conflito, otimize para o Carlos.
3. `docs/fluxos.md`: 12 telas, fluxos com tempo esperado e estados vazio, erro e sem conexão.
4. `docs/estruturadedados.md`: Personal, Aluno, HorarioFixo, Agendamento e Treino, com as regras de negócio.
5. `DESIGN.md`: cores, tipografia, espaçamento e componentes. Todo elemento visual segue este arquivo.
6. `docs/integracoes.md`: Supabase, offline, fotos, analytics, deploy.
7. `docs/metricas.md`: eventos que precisam ser registrados junto com cada ação.
8. `docs/decisoes.md`: decisões técnicas já tomadas. Não reabra sem motivo novo.

## Stack e comandos

- Stack: Expo (React Native) + TypeScript + Expo Router, NativeWind, TanStack Query com cache persistido, Supabase (Postgres, Auth, Storage), PostHog, Sentry, EAS Build.
- Instalar: `npm install`
- Banco local: `npx supabase start` e depois `npx supabase db reset` (aplica migrations e seed)
- Rodar: `npx expo start`
- Testar: `npm test` (Jest com jest-expo), `npm run typecheck` e `npm run lint`
- Validar o design: `npx @google/design.md lint DESIGN.md`
- Gerar o tema do NativeWind a partir do DESIGN.md: `npm run tema`
- Build de teste para Android: `npx eas build --profile preview --platform android`

## Regras de trabalho

- Construa uma funcionalidade por vez, na ordem do escopo em `docs/contexto.md`.
- Nada fora do escopo sem confirmar antes. Pagamento, app do aluno, ficha de treino e IA estão fora.
- Toda tela abre do cache e toda escrita passa pela fila offline. Nunca bloqueie a interface esperando a rede.
- Toda tabela nova nasce com RLS por `personal_id`. Sem exceção.
- Cor, fonte e espaçamento vêm do `DESIGN.md`. Não invente valor novo; se precisar, proponha e atualize o arquivo.
- Cada ação descrita em `docs/fluxos.md` dispara o evento de `docs/metricas.md` na mesma entrega.
- Mudou dado, tela, integração ou tecnologia? Atualize o doc correspondente na mesma entrega.
- Decisão técnica relevante vai para `docs/decisoes.md` com data, alternativa descartada e motivo.
