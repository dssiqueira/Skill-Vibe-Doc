# Integrações e infraestrutura

## Autenticação
- **Supabase Auth com telefone e código SMS** (OTP de 6 dígitos, validade de 10 minutos), SMS enviado pelo Twilio Verify configurado no Supabase.
- Sem senha e sem login social. O telefone verificado é o mesmo que o outro lado recebe depois do aceite. Motivo em `decisoes.md`.
- No primeiro acesso a pessoa escolhe o lado (`morador` ou `profissional`) e informa nome e email. O tipo não muda depois.
- Sessão de 30 dias, renovada a cada uso.
- Depois do MVP: login por WhatsApp (código pelo WhatsApp em vez de SMS), mais barato e mais familiar para o profissional.

## Banco de dados
- **Supabase Postgres com a extensão PostGIS.** Distância e raio calculados no banco com `ST_DWithin` em `geography`, em uma função `pedidos_elegiveis(profissional_id)` e outra `contar_cobertura(cep, categoria)`.
- Row Level Security em todas as tabelas:
  - `pedido`: morador lê e altera só os próprios; profissional lê só pela função `pedidos_elegiveis` e pelos pedidos em que tem proposta.
  - `proposta`: profissional lê e cria as próprias; morador lê as dos próprios pedidos.
  - `usuario.telefone` e `pedido.endereco_servico`: expostos à outra parte só pela view `contato_liberado`, que exige proposta `aceita` entre os dois.
  - `avaliacao`: leitura pública; criação só pelo morador do pedido `concluido`.
- Aceite de proposta numa função `aceitar_proposta(proposta_id)` com transação única (aceita uma, recusa as outras, muda o pedido).
- Expiração de 72 horas e aviso de 24 horas por `pg_cron`, a cada 15 minutos.
- Migrações versionadas em `supabase/migrations`.

## Arquivos
- **Supabase Storage**, bucket `perfis` (leitura pública, escrita só pelo dono da pasta `usuario_id/`).
- Foto de perfil e fotos de trabalho: JPG, PNG ou WebP, até 5 MB no envio. Redimensionadas no navegador para 800px no lado maior antes do upload; foto de perfil cortada em quadrado.
- Até 6 fotos de trabalho por profissional. Pedido não tem foto no MVP.

## APIs externas
- **ViaCEP**: CEP para logradouro, bairro e cidade, no Início público, no endereço do pedido e no cadastro do profissional. Gratuito, sem chave. (MVP)
- **Google Geocoding API**: endereço para latitude e longitude, uma vez por endereço salvo, chamada no servidor. Resultado gravado no banco; nunca geocodificar a cada busca. (MVP)
- **Resend**: emails transacionais com templates em React Email. (MVP)
  - Nova proposta recebida (para o morador).
  - Proposta aceita, com nome, telefone e endereço do morador (para o profissional).
  - Proposta recusada ou pedido cancelado (para o profissional).
  - Pedido novo elegível (para profissionais disponíveis): no máximo 1 email a cada 30 minutos por profissional, agrupando os pedidos do período; urgente sai na hora.
  - Pedido sem proposta em 24 horas e pedido expirado (para o morador).
- **WhatsApp**: só link `wa.me` com mensagem pronta; sem API. (MVP)
- **Pagamento**: nenhum no MVP. Depois: Stripe ou Mercado Pago com repasse ao profissional, só se o critério de sucesso for atingido.
- **Push e WhatsApp Business API**: depois do MVP, se a mediana do tempo até a primeira proposta passar de 2 horas.

## Ambiente e deploy
- **Vercel** para o Next.js; **Supabase** com dois projetos, `resolve-ai-staging` e `resolve-ai-prod`. Preview da Vercel aponta para staging.
- Variáveis de ambiente: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY` (só servidor), `GOOGLE_GEOCODING_API_KEY` (só servidor), `RESEND_API_KEY`, `NEXT_PUBLIC_POSTHOG_KEY`. Twilio fica configurado no painel do Supabase, não no app.
- Desenvolvimento local com `supabase start` (Postgres, Auth e Storage locais; SMS de teste com código fixo).

## Monitoramento
- **Sentry** para erros de navegador e servidor, sem telefone, email, endereço nem texto de pedido nos payloads (filtro `beforeSend`).
- **PostHog** para os eventos de `metricas.md`, com `usuario_id` e nunca telefone ou CEP completo.
- Alerta por email quando a taxa de erro de "Publicar pedido" ou "Enviar proposta" passar de 2% em 1 hora.
