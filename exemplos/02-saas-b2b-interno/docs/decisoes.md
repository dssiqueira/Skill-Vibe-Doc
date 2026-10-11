# Decisões técnicas

*A mais recente em cima. Antes de reabrir uma decisão, traga um motivo que não estava aqui.*

---

## 2026-03-18 Hospedar o app no servidor interno, não na Vercel

- **Contexto:** o produto não pode ser acessível fora da rede interna e da VPN.
- **Decisão:** Next.js em modo `standalone`, em contêiner Docker no servidor interno, atrás do proxy reverso da empresa. Supabase continua na nuvem, protegido por SSO e RLS.
- **Alternativas descartadas:** Vercel com proteção por IP (o recurso de lista de IPs exige plano Enterprise, caro para uma ferramenta de 600 pessoas); Vercel com proteção por senha (não restringe rede e cria uma segunda senha para o Marcos); Supabase auto-hospedado (mais uma peça para 4 analistas manterem, sem ganho real com RLS bem feito).
- **Onde entra o humano:** a equipe de infraestrutura libera a porta no proxy e mantém o certificado interno.

## 2026-03-12 Sem IA na triagem e na prioridade

- **Contexto:** surgiu a ideia de usar um modelo de linguagem para sugerir categoria e prioridade a partir da descrição.
- **Decisão:** o solicitante escolhe categoria e prioridade com textos de ajuda; o analista corrige na fila. A ordenação da fila é uma regra fixa (prioridade, depois data).
- **Alternativas descartadas:** classificação automática por IA (com 250 chamados por mês e 4 categorias, o analista reclassifica em 2 cliques; a IA adicionaria custo, envio de texto de chamado para fora e um erro difícil de explicar ao solicitante); resposta automática a chamados de senha (o reset já é self-service no portal da Microsoft).
- **Nível de autonomia:** sem IA. O degrau mais baixo resolve: o problema é falta de fila e histórico, não falta de inteligência. Revisar se o volume passar de 1.000 chamados por mês ou se a calibração de prioridade ficar fora da meta por 2 meses seguidos.
- **Onde entra o humano:** o analista decide prioridade final e responsável em todo chamado.

## 2026-03-10 Login só por SSO da Microsoft, com uma conta de emergência

- **Contexto:** a empresa usa Microsoft 365 e o Marcos não aceita criar mais uma senha.
- **Decisão:** Supabase Auth com provedor Entra ID, restrito ao tenant, e perfil derivado dos grupos `TI-Analistas` e `TI-Admin`. Uma única conta de email e senha, com MFA, para o admin entrar se o SSO cair.
- **Alternativas descartadas:** email e senha para todos (mais uma senha, mais pedido de reset no próprio TI); Google Workspace SSO (a empresa não usa Google); NextAuth com Entra ID (duplicaria sessão com o Supabase e complicaria o RLS, que depende do `auth.uid()`).

## 2026-03-05 Supabase como banco, auth e storage

- **Contexto:** um dev part-time constrói e o time de TI mantém; regras de visibilidade (solicitante vê só o seu, comentário interno) são o coração da segurança.
- **Decisão:** Supabase (Postgres, Auth, Storage, Realtime e Edge Functions) no plano Pro, região São Paulo.
- **Alternativas descartadas:** API própria em Node com Postgres gerenciado (mais código para escrever e manter, e as regras de acesso ficariam só na aplicação); Firebase (regras de acesso menos expressivas para o caso "comentário interno" e relatórios do Painel mais difíceis sem SQL); Jira Service Management (licença por analista aceitável, mas a experiência do solicitante não técnico foi o motivo das reclamações num teste anterior; continua como plano B no critério de morte).

## 2026-03-05 Email em texto simples pela Resend

- **Contexto:** o solicitante precisa saber do andamento sem entrar no sistema.
- **Decisão:** Resend, email em texto simples com link para o chamado, disparado por Edge Function.
- **Alternativas descartadas:** SendGrid (configuração e painel mais pesados para o volume de cerca de 1.000 emails por mês); envio pelo Exchange da empresa via SMTP (depende de liberação de relay pela infraestrutura, que levaria semanas); notificação no Teams (fica para depois do MVP; email já resolve e não exige app registrado no tenant).
