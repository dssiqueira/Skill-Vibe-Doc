# Balcão TI

Ferramenta interna onde todo pedido de TI (acesso, suporte, equipamento) vira um chamado com fila, prioridade, responsável e histórico. Para os 600 colaboradores que pedem e para os 4 analistas de TI que atendem, só na rede interna ou VPN.

## Antes de mexer em qualquer coisa

Leia, nesta ordem:

1. `docs/contexto.md`: problema, público, escopo, o que não é, critério de sucesso e de morte.
2. `docs/personas.md`: Marcos (solicitante) e Rafael (analista). Em conflito, otimize para Marcos, exceto nas telas exclusivas do analista.
3. `docs/fluxos.md`: telas das duas visões, fluxos e estados.
4. `docs/estruturadedados.md`: Usuario, Chamado, Comentario, Anexo, HistoricoStatus, Evento e regras de negócio.
5. `DESIGN.md`: cores, tipografia, espaçamento e componentes. Todo elemento visual segue este arquivo.
6. `docs/integracoes.md`: SSO Microsoft, Supabase, Resend, deploy interno.
7. `docs/metricas.md`: eventos que precisam ser registrados.
8. `docs/decisoes.md`: decisões técnicas já tomadas. Não reabra sem motivo novo.

## Stack e comandos

- Stack: Next.js 15 (App Router) com TypeScript, Tailwind CSS, Supabase (Postgres, Auth com Entra ID, Storage, Realtime, Edge Functions), Resend, Docker no servidor interno.
- Instalar: `pnpm install`
- Banco local: `pnpm supabase start` e `pnpm supabase db reset` (aplica migrations e seed)
- Rodar: `pnpm dev`
- Testar: `pnpm test` (Vitest) e `pnpm test:rls` (testes das políticas de acesso)
- Tipos do banco: `pnpm supabase gen types typescript --local > src/lib/database.types.ts`
- Tema do Tailwind: `npx @google/design.md export --format css-tailwind DESIGN.md`

## Regras de trabalho

- Construa uma funcionalidade por vez, na ordem do escopo em `docs/contexto.md`.
- Nada fora do escopo sem confirmar antes. Em especial: sem SLA, sem aprovação de compra, sem IA.
- Regra de visibilidade vai para o RLS e ganha teste em `pnpm test:rls`. Esconder só na tela não conta.
- Toda mudança de status, prioridade ou responsável passa pela função do banco que grava o HistoricoStatus.
- Cor, fonte e espaçamento vêm do `DESIGN.md`. Não invente valor novo; se precisar, proponha e atualize o arquivo.
- Mudou dado, tela, integração ou tecnologia? Atualize o doc correspondente na mesma entrega.
- Decisão técnica relevante vai para `docs/decisoes.md` com data, alternativa descartada e motivo.
