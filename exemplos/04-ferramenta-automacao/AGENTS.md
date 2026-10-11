# Embarque

Ferramenta interna que automatiza o onboarding de clientes B2B: do formulário do backoffice ao contrato assinado e aos acessos criados nos sistemas internos, com log de auditoria de cada passo. É para o backoffice operar e o comercial acompanhar; o cliente final nunca acessa.

## Antes de mexer em qualquer coisa

Leia, nesta ordem:

1. `docs/contexto.md`: processo manual de hoje, escopo, o que não é, critério de sucesso e de morte.
2. `docs/personas.md`: Fernanda (backoffice, principal) e Bruno (comercial, só lê).
3. `docs/fluxos.md`: telas, fluxos da esteira e estados de erro.
4. `docs/estruturadedados.md`: entidades, as seis etapas e as regras de tentativa e idempotência.
5. `DESIGN.md`: cores, tipografia, espaçamento e componentes. Todo elemento visual segue este arquivo.
6. `docs/integracoes.md`: Supabase, D4Sign, Sistemas 1, 2 e 3, Resend, ambientes.
7. `docs/metricas.md`: eventos que vão para o log de auditoria.
8. `docs/decisoes.md`: decisões já tomadas, incluindo o degrau de autonomia de cada etapa. Não reabra sem motivo novo.

## Stack e comandos

- Stack: Next.js (App Router) com TypeScript e Tailwind na Vercel; Supabase (Postgres, Auth, Realtime, Edge Functions, pg_cron); D4Sign; Resend.
- Instalar: `pnpm install`
- Banco e funções locais: `supabase start` e `supabase functions serve`
- Rodar: `pnpm dev`
- Testar: `pnpm test` (unitários com Vitest) e `pnpm test:e2e` (Playwright contra staging)
- Migrações: `supabase migration new <nome>` e `supabase db push`
- Tema do Tailwind: `npx @google/design.md export --format css-tailwind DESIGN.md`

## Regras de trabalho

- Construa uma funcionalidade por vez, na ordem do escopo em `docs/contexto.md`.
- Nada fora do escopo sem confirmar antes.
- Nenhuma ação automática sem linha em LogAuditoria. Nenhuma chamada externa sem chave de idempotência.
- Lógica de etapa vive nas Edge Functions, nunca no frontend.
- Não adicione IA, RPA ou nova automação de etapa sem registrar o degrau e o ponto humano em `docs/decisoes.md`.
- Em `staging`, só sandbox e homologação. Nunca aponte para sistema real.
- Cor, fonte e espaçamento vêm do `DESIGN.md`. Não invente valor novo; se precisar, proponha e atualize o arquivo.
- Mudou dado, tela, integração ou tecnologia? Atualize o doc correspondente na mesma entrega.
- Decisão técnica relevante vai para `docs/decisoes.md` com data, alternativa descartada e motivo.
