# Integrações e infraestrutura

## Aplicativo
- **Expo (React Native) com TypeScript**, Expo Router para navegação. Um código para Android e iOS. Motivo em `decisoes.md`.
- **Estilo:** NativeWind (Tailwind para React Native), com o tema gerado a partir do `DESIGN.md` (`npm run tema`, que roda `npx @google/design.md export --format json-tailwind DESIGN.md` e grava o `theme.extend` usado pelo `tailwind.config.js`; NativeWind usa Tailwind v3). Nenhuma cor ou espaçamento escrito à mão fora do tema.
- **Estado do servidor e cache:** TanStack Query com persistência local (ver "Offline e sincronização").
- **Estado de interface:** Zustand, só para o que não vem do banco (filtro selecionado, dia aberto na Agenda). Nada de Redux.
- **Formulários:** React Hook Form com validação em Zod; os mesmos esquemas validam antes de enfileirar offline.
- Fontes carregadas com `expo-font`, embutidas no app (sem baixar da rede na abertura).

## Autenticação
- **Supabase Auth com e-mail e senha.** Cadastro com nome, e-mail e senha (mínimo 8 caracteres).
- Confirmação de e-mail não bloqueia a entrada no MVP: a conta funciona na hora e o e-mail de confirmação é enviado em segundo plano.
- Recuperação de senha por link no e-mail, que abre o app por deep link (`treinou://nova-senha`).
- Sessão persistida no aparelho com `expo-secure-store`, renovada automaticamente; o personal só entra de novo se ficar 60 dias sem abrir o app ou se sair.
- **Depois do MVP:** login com Google e Apple, se o funil de cadastro mostrar perda na tela de senha.

## Banco de dados
- **Supabase (PostgreSQL gerenciado)**, região São Paulo (`sa-east-1`).
- Tabelas espelham `estruturadedados.md`: `personais`, `alunos`, `horarios_fixos`, `agendamentos`, `treinos`. Migrations versionadas em `supabase/migrations/`.
- **Row Level Security ligado em todas as tabelas.** Política única por tabela: `personal_id = auth.uid()` para ler, criar, editar e apagar. A interface nunca é a única barreira.
- Restrições no banco, não só no app: `treinos.agendamento_id` único; índice único parcial em `agendamentos (aluno_id, data local)` para `status = 'agendado'`; `check` de `data_hora <= now()` em `treinos` com tolerância de 5 minutos para relógio do celular.
- **Geração de agendamentos:** função `gerar_agendamentos()` em SQL, chamada ao salvar um horário fixo e diariamente às 3h por `pg_cron`, mantendo 14 dias à frente.
- **Backup:** o backup diário do Supabase basta para o beta. Exportação de dados pelo personal fica para depois do MVP.

## Offline e sincronização
- **Leitura:** cache do TanStack Query persistido no aparelho (MMKV). Ficam em cache: alunos ativos, agendamentos de 7 dias atrás a 14 dias à frente, horários fixos vigentes e os últimos 30 treinos de cada aluno.
- **Escrita:** toda criação e edição entra numa fila local de mutações, com o UUID gerado no aparelho. A fila sobe em ordem quando a conexão volta, detectada por `@react-native-community/netinfo` e por nova tentativa a cada 30 segundos.
- **Conflito:** última edição ganha, por `atualizado_em`. Sem merge campo a campo.
- **Erro ao subir** (ex.: regra de dia ocupado violada): o item sai da fila, fica marcado como "Não salvo" na interface e espera a decisão do personal.
- **Fotos offline:** guardadas no sistema de arquivos do app e enviadas junto com a fila.

## Arquivos
- **Supabase Storage**, bucket privado `fotos`.
- Caminhos: `fotos/{personal_id}/perfil.jpg` e `fotos/{personal_id}/alunos/{aluno_id}.jpg`. A política do bucket libera só o prefixo do próprio `personal_id`.
- No aparelho, antes de subir: recorte quadrado, 400 x 400 px, JPEG qualidade 0,8 (`expo-image-manipulator`). Resultado típico abaixo de 80 KB. Aceita JPG, PNG, HEIC e WEBP na entrada; limite de 10 MB antes do recorte.
- Exibição com `expo-image` e URL assinada de 7 dias, em cache no aparelho.
- Sem foto: avatar com as iniciais, cor de fundo fixa definida no DESIGN.md (não varia por aluno).

## APIs e recursos do aparelho
- **WhatsApp** (MVP): link `https://wa.me/55{telefone}`, sem API e sem mensagem pronta.
- **Telefone** (MVP): link `tel:`.
- **Contatos** (MVP): `expo-contacts`, só leitura, só quando o personal toca em "Importar dos contatos".
- **Câmera e galeria** (MVP): `expo-image-picker`.
- **Google Maps / autocompletar endereço:** fora do MVP. Local é texto livre com sugestão dos locais já usados.
- **WhatsApp Business API** (lembrete para o aluno, confirmação de presença): fora do MVP.

## Notificações
- **Fora do MVP.** Candidatas para a versão seguinte, via Expo Notifications: lembrete 30 minutos antes do treino e aviso semanal de alunos sumidos.

## Pagamentos
- **Fora do MVP.** Não há cobrança de aluno nem assinatura do personal no beta. O plano Pro, quando vier, usa assinatura dentro das lojas (Google Play Billing e App Store) via RevenueCat.

## Analytics
- **PostHog** (`posthog-react-native`), instância na nuvem da UE. Eventos de `metricas.md`, com fila própria que funciona offline.
- Identificação só por `personal_id`. Sem nome, e-mail, telefone ou texto de observação nos eventos.

## Ambiente e deploy
- **Ambientes:** `dev` (Supabase local via CLI, com seed de 1 personal, 15 alunos e 4 semanas de treinos), `staging` (projeto Supabase separado, usado pelo beta interno) e `prod`.
- **Variáveis de ambiente** (prefixo `EXPO_PUBLIC_` só para o que pode ir no app): `EXPO_PUBLIC_SUPABASE_URL`, `EXPO_PUBLIC_SUPABASE_ANON_KEY`, `EXPO_PUBLIC_POSTHOG_KEY`, `EXPO_PUBLIC_SENTRY_DSN`. A `service_role` do Supabase nunca entra no app nem no repositório.
- **Build e distribuição:** EAS Build. Beta pelo teste interno da Google Play (prioridade, persona principal é Android) e TestFlight. Correções de JavaScript via EAS Update no canal `staging` antes de `prod`.
- **CI:** GitHub Actions roda lint, tipos, testes e `npx @google/design.md lint DESIGN.md` em todo pull request.

## Monitoramento
- **Sentry** (`@sentry/react-native`) para erros e travamentos, com source maps enviados pelo EAS.
- Registra falhas de sincronização com tipo de entidade e código de erro, nunca o conteúdo.
- Sem dado pessoal nos logs: nada de nome, telefone, e-mail completo ou observação.
- Acompanhar: tempo de abertura até a Agenda visível (meta: menos de 1,5 s em Android intermediário com cache) e taxa de itens com erro na fila.

---

*A IA deve usar essas especificações para configurar o projeto. Priorizar simplicidade e velocidade no MVP. Não over-engineer.*
