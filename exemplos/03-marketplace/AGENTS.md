# Resolve Aí

Marketplace de serviços domésticos em Campinas: o morador publica um pedido (elétrica, hidráulica, limpeza, pintura, pequenos reparos) e profissionais autônomos da região mandam propostas com valor e prazo. Os dois lados são produto: a Cláudia precisa escolher rápido e com segurança, o Seu João precisa achar trabalho sem burocracia.

## Antes de mexer em qualquer coisa

Leia, nesta ordem:

1. `docs/contexto.md`: problema dos dois lados, escopo, o que não é, critério de sucesso e de morte.
2. `docs/personas.md`: Cláudia (demanda) e Seu João (oferta). Em conflito, otimize para a Cláudia.
3. `docs/fluxos.md`: telas de cada lado, fluxos e estados.
4. `docs/estruturadedados.md`: entidades, status do pedido e regras de visibilidade entre os lados.
5. `DESIGN.md`: cores, tipografia, espaçamento e componentes. Todo elemento visual segue este arquivo.
6. `docs/integracoes.md`: auth por SMS, Supabase com PostGIS e RLS, Resend, ViaCEP, Geocoding.
7. `docs/metricas.md`: eventos que precisam ser registrados.
8. `docs/decisoes.md`: decisões técnicas já tomadas. Não reabra sem motivo novo.

## Stack e comandos

- Stack: Next.js (App Router) com TypeScript, Supabase (Postgres com PostGIS, Auth, Storage, pg_cron), Tailwind, Resend, Vercel. Gerenciador: pnpm.
- Instalar: `pnpm install`
- Banco local: `supabase start` e `supabase db reset` (aplica migrações e seed)
- Rodar: `pnpm dev`
- Testar: `pnpm test` (Vitest) e `pnpm test:e2e` (Playwright)
- Tipos do banco: `supabase gen types typescript --local > src/lib/database.types.ts`
- Tema: `npx @google/design.md export --format css-tailwind DESIGN.md > src/app/theme.css`

## Regras de trabalho

- Construa uma funcionalidade por vez, na ordem do escopo em `docs/contexto.md`, sempre dos dois lados (pedido sem tela de proposta não está pronto).
- Nada fora do escopo sem confirmar antes.
- Toda regra de visibilidade entre morador e profissional vive em RLS ou função do banco, nunca só no front. Telefone e endereço só depois do aceite.
- Cor, fonte e espaçamento vêm do `DESIGN.md`. Não invente valor novo; se precisar, proponha e atualize o arquivo.
- Mudou dado, tela, integração ou tecnologia? Atualize o doc correspondente na mesma entrega.
- Decisão técnica relevante vai para `docs/decisoes.md` com data, alternativa descartada e motivo.
