# Página Pronta

Ferramenta web que gera uma landing page completa a partir de um briefing curto e do DESIGN.md da marca do usuário: a IA escreve o texto, os templates aplicam a marca e o usuário exporta um HTML pronto para publicar. Feita para founders que validam ideias e profissionais autônomos sem site.

## Antes de mexer em qualquer coisa

Leia, nesta ordem:

1. `docs/contexto.md`: problema, público, escopo, o que não é, critério de sucesso e de morte.
2. `docs/personas.md`: Rodrigo (principal) e Mariana. Em conflito, otimize para o Rodrigo; todo fluxo funciona no celular por causa da Mariana.
3. `docs/fluxos.md`: telas, fluxos e estados, incluindo o passo Marca do briefing.
4. `docs/estruturadedados.md`: Usuario, Marca, Briefing, LandingPage e regras de crédito.
5. `DESIGN.md`: a cara da interface do produto. Atenção: a página gerada segue o DESIGN.md da Marca do usuário, nunca este.
6. `docs/integracoes.md`: Supabase, modelo de linguagem via API, Stripe, Resend, Vercel e o uso do DESIGN.md da marca no gerador.
7. `docs/metricas.md`: eventos que precisam ser registrados.
8. `docs/decisoes.md`: decisões já tomadas (IA só escreve texto, guardrails, custo). Não reabra sem motivo novo.

## Stack e comandos

- Stack: Next.js (App Router) com TypeScript, Tailwind CSS (tema gerado do DESIGN.md), Supabase (Auth, Postgres, Storage), modelo de linguagem via API, Zod, Stripe, Resend, Sentry, Vercel.
- Instalar: `npm install`
- Banco local: `npx supabase start` e `npx supabase db reset`
- Rodar: `npm run dev`
- Testar: `npm test` (Vitest, inclui os testes de esquema e de guardrail do gerador) e `npm run test:e2e` (Playwright)
- Tema: `npx @google/design.md export --format css-tailwind DESIGN.md > app/theme.css`

## Regras de trabalho

- Construa uma funcionalidade por vez, na ordem do escopo em `docs/contexto.md`.
- Nada fora do escopo sem confirmar antes.
- A IA do produto só devolve JSON validado; nunca gere HTML, CSS ou cor a partir da resposta do modelo.
- Cor, fonte e espaçamento da interface vêm do `DESIGN.md`. Não invente valor novo; se precisar, proponha e atualize o arquivo.
- Mudou dado, tela, integração ou tecnologia? Atualize o doc correspondente na mesma entrega.
- Decisão técnica relevante vai para `docs/decisoes.md` com data, alternativa descartada e motivo.
