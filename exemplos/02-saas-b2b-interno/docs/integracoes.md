# Integrações e infraestrutura

## Autenticação
- **Microsoft Entra ID (antigo Azure AD)** via Supabase Auth (provedor `azure`), restrito ao tenant da empresa. Só emails do domínio corporativo entram.
- O perfil vem dos grupos do Entra ID no login (`TI-Analistas` vira `analista`, `TI-Admin` vira `admin`, o resto é `solicitante`); o admin pode sobrescrever na tela Usuários.
- Sem email e senha para colaboradores. Existe uma única conta de emergência do admin, com senha forte e MFA, para quando o SSO cair (ver `docs/decisoes.md`).
- Sessão expira em 8 horas.
- Depois do MVP: Google Workspace SSO só se a empresa mudar de provedor.

## Banco de dados
- **Supabase Postgres**, região São Paulo (`sa-east-1`).
- Regras de acesso em RLS: solicitante lê e cria só os próprios chamados, comentários públicos e anexos; analista e admin leem tudo; só analista e admin alteram status, prioridade e responsável. Comentários internos filtrados por RLS, não pelo frontend.
- Mudanças de status, prioridade e responsável passam por função do banco (`rpc`) que grava o HistoricoStatus na mesma transação.
- Supabase Realtime na tabela de chamados para a Fila atualizar sem recarregar.
- Migrations versionadas em `supabase/migrations`, nunca alteração manual no painel.

## Arquivos
- **Supabase Storage**, bucket privado `anexos`, caminho `chamado_id/arquivo`.
- Até 10 MB por arquivo, 5 por chamado. Tipos: jpg, png, pdf, docx (validado no navegador e na política do bucket).
- Download por URL assinada de 10 minutos.

## Notificações
- **Resend** para email transacional, remetente `ti@empresa.com.br` (domínio verificado com SPF e DKIM).
- Email em texto simples, com assunto padrão "[Chamado #1042] título" e link direto para o chamado.
- Eventos que disparam email:
  - novo chamado aberto: analistas (resumo a cada 30 minutos para não lotar a caixa), exceto crítico;
  - chamado crítico: todos os analistas ativos, na hora;
  - mudança de status: solicitante;
  - comentário público do TI: solicitante;
  - chamado aberto em nome do colaborador: o colaborador.
- Comentário interno nunca gera email.
- Envio feito por Supabase Edge Function disparada por database webhook, com até 3 tentativas. O resumo de 30 minutos roda por `pg_cron` chamando a mesma função.
- Depois do MVP: notificação no Microsoft Teams via webhook do canal do TI.

## APIs externas
- Microsoft Graph: não usar no MVP. Nome, email e departamento vêm do token do SSO.
- Microsoft Teams: depois do MVP.

## Pagamentos
- Não necessário. Ferramenta interna sem cobrança.

## Ambiente e deploy
- App Next.js em modo `standalone`, em contêiner Docker no servidor interno da empresa, atrás do proxy reverso que só aceita a rede interna e a VPN.
- Dois projetos Supabase: `balcao-ti-staging` e `balcao-ti-prod`.
- Variáveis: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY` (só no servidor), `RESEND_API_KEY`, `APP_URL`.
- Deploy pelo pipeline do GitHub Actions: build da imagem, push para o registro interno, atualização no servidor. Staging a cada merge na `main`, produção por tag.

## Monitoramento
- Logs do contêiner no servidor de logs da empresa; erros do frontend e do servidor com Sentry (plano gratuito), sem texto de chamado nem anexo no payload.
- Alerta no email do admin se a Edge Function de email falhar 3 vezes seguidas.
- Backup diário do Supabase (padrão do plano Pro), retenção de 7 dias.
