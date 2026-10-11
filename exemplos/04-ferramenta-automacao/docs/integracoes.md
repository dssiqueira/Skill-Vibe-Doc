# Integrações e infraestrutura

## Autenticação
- Supabase Auth com login Google restrito ao domínio do Google Workspace da empresa. Sem senha própria.
- Perfis em `Usuario.perfil`: `backoffice` opera tudo; `comercial` só lê. Primeiro login entra como `comercial`; um backoffice promove outro na tela de usuários do painel do Supabase no MVP (tela própria fica para depois).
- Sessão de 30 dias com refresh token.

## Banco de dados
- Supabase Postgres. É também o orquestrador da esteira (ver `decisoes.md`): o estado de cada etapa mora na tabela EtapaOnboarding.
- Row Level Security em todas as tabelas: comercial lê Cliente, Onboarding e EtapaOnboarding (sem `erro_detalhe`, via view); backoffice lê e escreve. LogAuditoria só aceita `insert`, com `update` e `delete` revogados para todos os papéis, inclusive `service_role` via trigger que bloqueia.
- Realtime ligado em Onboarding e EtapaOnboarding para o Painel atualizar sozinho.

## Orquestração da esteira
- Supabase Edge Functions (Deno), uma por etapa automática: `enviar-contrato`, `criar-acesso-sistema1`, `criar-acesso-sistema2`, `notificar-conclusao`, mais `webhook-d4sign`.
- `pg_cron` roda a cada minuto e chama as funções das etapas em `pendente` cuja anterior está `concluida`, e das etapas com `proxima_tentativa_em` vencida.
- Cada função: grava log, chama o sistema externo com chave de idempotência, grava resultado e log. Nada de lógica de etapa no frontend.

## Arquivos
- Não armazena arquivo no MVP. O contrato assinado fica na D4Sign, e o Detalhe linka para o envelope.
- Depois: cópia do PDF assinado no Supabase Storage, bucket privado.

## APIs externas
- **D4Sign** (MVP): cria documento a partir do modelo por plano, envia para o `email_contato` e notifica por webhook quando assinado. Webhook validado por token secreto na URL e conferência do id do envelope. Ver `decisoes.md`.
- **Sistema 1** (MVP): API REST interna, `POST /api/usuarios`, autenticação por token de serviço. Idempotência pelo `cnpj` + `email_contato`: antes de criar, consulta se já existe.
- **Sistema 2** (MVP): API REST interna, `POST /api/contas`, aceita header `Idempotency-Key` (usamos o id da etapa).
- **Sistema 3** (MVP, manual): legado sem API. A ferramenta só gera o checklist e registra quem fez. Ver `decisoes.md`.
- **Resend** (MVP): e-mails transacionais. Para backoffice: erro em etapa, tarefa manual pendente, assinatura parada há 5 dias úteis. Para comercial: onboarding concluído. Para o cliente: credenciais de acesso ao final.
- **Slack ou Teams** (depois): mesmos avisos num canal do backoffice.
- **CRM** (depois): criar onboarding a partir do negócio ganho, sem formulário.

## Ambiente e deploy
- Frontend Next.js na Vercel; Edge Functions e banco no Supabase.
- Dois ambientes: `staging` (D4Sign sandbox, Sistemas 1 e 2 de homologação) e `producao`. Nenhuma chamada a sistema real a partir de `staging`.
- Variáveis: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY`, `D4SIGN_TOKEN`, `D4SIGN_CRYPT_KEY`, `D4SIGN_WEBHOOK_SECRET`, `SISTEMA1_API_URL`, `SISTEMA1_TOKEN`, `SISTEMA2_API_URL`, `SISTEMA2_TOKEN`, `RESEND_API_KEY`. Segredos das Edge Functions via `supabase secrets set`, nunca no repositório.

## Monitoramento
- Logs das Edge Functions no painel do Supabase, sem dado pessoal além de ids.
- Sentry no frontend e nas Edge Functions para exceção não tratada.
- A própria tabela LogAuditoria é a trilha de auditoria de negócio; retenção mínima de 5 anos.
- Alerta por e-mail ao backoffice se o `pg_cron` não rodar por mais de 10 minutos (função de heartbeat).
