# Integrações e infraestrutura

## Autenticação
- Supabase Auth com Google (principal) e e-mail e senha.
- Gerar sem conta é permitido: a sessão anônima recebe um id em cookie e gera 1 página (limite de 3 por IP por dia).
- Conta é exigida para salvar, exportar e guardar marcas; ao criar conta, briefing, Marca e página da sessão migram para o usuário.
- Depois do MVP: login por link mágico.

## Banco de dados
- Supabase Postgres. Tabelas: `usuarios`, `marcas`, `briefings`, `landing_pages` (campos em `docs/estruturadedados.md`).
- Row Level Security em todas as tabelas: cada usuário lê e escreve só o que tem o próprio `usuario_id`. Linhas de sessão anônima só são acessadas pelo servidor com a service role.
- Zerar `geracoes_no_mes` no dia 1: cron do Supabase (pg_cron).

## Arquivos
- Supabase Storage, bucket privado `logos`: PNG ou SVG, até 1 MB. SVG é sanitizado no upload (remove script, `on*` e referências externas).
- O HTML exportado embute o logo (SVG inline ou PNG em base64) e todo o CSS: um arquivo só, sem dependência do nosso servidor.
- HTML e DESIGN.md ficam como texto no banco; não vão para o storage.

## Identidade visual da marca (DESIGN.md)
- Entrada do gerador: cada página é montada a partir de uma Marca, que é um DESIGN.md válido no padrão aberto do Google (`@google/design.md`).
- Importar: o usuário sobe ou cola o arquivo; o servidor roda o lint da biblioteca `@google/design.md`, interpreta o frontmatter e guarda arquivo e tokens.
- Montar: o produto escreve o DESIGN.md a partir de cor principal, cor de apoio, fonte e estilo de canto, com código determinístico (sem IA), e valida com o mesmo lint.
- Uso no gerador: os tokens do frontmatter viram variáveis CSS do template da página; o texto das seções `## Overview` e `## Do's and Don'ts` vai para a IA como contexto de tom, nunca como instrução de cor ou layout.
- Exportar: o DESIGN.md usado vai junto com o HTML, para o usuário reaproveitar no repositório do produto e nos agentes de código.
- Fontes: só as do Google Fonts, carregadas por link no HTML exportado. Fonte fora da lista vira a fonte mais próxima da mesma categoria, com aviso.
- Depois do MVP: extrair a marca de um site por URL.

## APIs externas
- **Modelo de linguagem via API (MVP):** escreve os textos e escolhe a ordem das seções. Recebe o briefing e o contexto de tom da Marca; devolve JSON no esquema `conteudo_gerado`, validado com Zod no servidor. Uma chamada por geração, saída limitada a 2.500 tokens, timeout de 20 segundos, uma nova tentativa se o JSON vier inválido. A chave fica só no servidor. Custo, guardrails e escolha do modelo em `docs/decisoes.md`.
- **Stripe (MVP):** Checkout para assinar o pro, Customer Portal para gerenciar, webhook `customer.subscription.*` atualiza `usuarios.plano`.
- **Resend (MVP):** e-mails de boas-vindas, aviso quando restar 1 geração no mês free e aviso de teto de uso justo no pro.

## Ambiente e deploy
- Vercel para o app Next.js; geração roda numa Route Handler com `maxDuration` de 30 segundos.
- Ambientes: `development` (Supabase local via CLI), `preview` (projeto Supabase de staging, um por PR na Vercel) e `production`.
- Variáveis: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY`, `LLM_API_KEY`, `LLM_MODEL`, `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `RESEND_API_KEY`, `SENTRY_DSN`.
- O nome do modelo vem de `LLM_MODEL`; trocar de modelo é configuração, não código.

## Monitoramento
- Sentry para erros de front e servidor, sem payload de briefing nem de texto gerado.
- Log por geração: `pagina_id`, tokens de entrada e saída, `custo_estimado_centavos`, `tempo_ms`, motivo de falha. Nunca o conteúdo.
- Alerta por e-mail (Resend) para o time se a taxa de `geracao_falhou` passar de 5% em uma hora ou se o custo diário de IA passar de R$ 150.
