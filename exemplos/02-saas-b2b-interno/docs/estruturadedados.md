# Estrutura de dados

## Entidade: Usuario
Um colaborador da empresa que já entrou pelo menos uma vez com a conta Microsoft.

**Campos:**
- `id` (uuid, único; o mesmo id do Supabase Auth)
- `nome` (texto, obrigatório; vem do Entra ID)
- `email` (texto, obrigatório, único; sempre do domínio corporativo)
- `departamento` (texto, opcional; vem do Entra ID)
- `perfil` (enum, obrigatório: `solicitante` | `analista` | `admin`; padrão `solicitante`)
- `ativo` (boolean, obrigatório; padrão `true`)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Tem muitos Chamados como solicitante.
- Tem muitos Chamados como analista responsável.
- Tem muitos Comentarios, Anexos e registros de HistoricoStatus como autor.

---

## Entidade: Chamado
Um pedido de TI, do momento em que é aberto até ser resolvido ou cancelado.

**Campos:**
- `id` (uuid, único)
- `numero` (inteiro sequencial, único; o que aparece na tela como "#1042")
- `titulo` (texto, obrigatório, até 120 caracteres)
- `descricao` (texto longo, obrigatório)
- `categoria` (enum, obrigatório: `acesso` | `suporte` | `equipamento` | `outro`)
- `prioridade` (enum, obrigatório: `baixa` | `media` | `alta` | `critica`; padrão `media`)
- `status` (enum, obrigatório: `aberto` | `em_andamento` | `aguardando_solicitante` | `resolvido` | `cancelado`; padrão `aberto`)
- `solicitante_id` (uuid, obrigatório, referência a Usuario)
- `aberto_por_id` (uuid, obrigatório, referência a Usuario; igual ao solicitante, ou o analista que registrou em nome dele)
- `analista_id` (uuid, opcional até a atribuição, referência a Usuario com perfil `analista` ou `admin`)
- `chamado_origem_id` (uuid, opcional, referência a Chamado; preenchido quando o chamado continua um resolvido)
- `criado_em` (timestamp, obrigatório)
- `atualizado_em` (timestamp, obrigatório)
- `resolvido_em` (timestamp, opcional; preenchido ao entrar em `resolvido`)

**Relacionamentos:**
- Pertence a um Usuario solicitante e, depois de atribuído, a um Usuario analista.
- Tem muitos Comentarios, Anexos e registros de HistoricoStatus.
- Pode continuar outro Chamado (`chamado_origem_id`).

---

## Entidade: Comentario
Uma mensagem no chamado, pública (o solicitante vê) ou interna (só o TI vê).

**Campos:**
- `id` (uuid, único)
- `chamado_id` (uuid, obrigatório)
- `autor_id` (uuid, obrigatório)
- `texto` (texto longo, obrigatório)
- `visivel_para_solicitante` (boolean, obrigatório; padrão `true`)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Pertence a um Chamado e a um Usuario autor.

---

## Entidade: Anexo
Arquivo enviado junto com o chamado (print, PDF, documento).

**Campos:**
- `id` (uuid, único)
- `chamado_id` (uuid, obrigatório)
- `autor_id` (uuid, obrigatório)
- `nome_arquivo` (texto, obrigatório)
- `caminho_storage` (texto, obrigatório; caminho no bucket privado, nunca URL pública)
- `tamanho_bytes` (inteiro, obrigatório; até 10 MB)
- `tipo_mime` (texto, obrigatório)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Pertence a um Chamado e a um Usuario autor.

---

## Entidade: HistoricoStatus
Cada mudança de status, prioridade ou responsável de um chamado. Alimenta a linha do tempo do detalhe e as métricas de tempo.

**Campos:**
- `id` (uuid, único)
- `chamado_id` (uuid, obrigatório)
- `autor_id` (uuid, obrigatório)
- `campo` (enum, obrigatório: `status` | `prioridade` | `analista`)
- `valor_anterior` (texto, opcional)
- `valor_novo` (texto, obrigatório)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Pertence a um Chamado e a um Usuario autor.

---

## Entidade: Evento
Registro de uso para as métricas de `docs/metricas.md`. Não aparece em nenhuma tela além do Painel, e só agregado.

**Campos:**
- `id` (uuid, único)
- `nome` (texto, obrigatório; um dos eventos de `docs/metricas.md`, em `snake_case`)
- `usuario_id` (uuid, obrigatório; quem executou a ação)
- `chamado_id` (uuid, opcional; vazio em `formulario_iniciado`)
- `dados` (jsonb, obrigatório; os campos de cada evento)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Pertence a um Usuario e, quando houver, a um Chamado.

---

## Regras de negócio

### Sobre Usuario
- O usuário é criado no primeiro login. O perfil vem do grupo do Entra ID (`TI-Analistas` vira `analista`, `TI-Admin` vira `admin`); o admin pode sobrescrever na tela de usuários.
- Usuário com `ativo = false` não entra no sistema, mas seus chamados continuam visíveis para o TI.

### Sobre Chamado
- Solicitante vê só os chamados em que é `solicitante_id`. Analista e admin veem todos. A regra vale no banco (RLS), não só na tela.
- Só analista e admin mudam status, prioridade e responsável. O solicitante só pode cancelar o próprio chamado enquanto ele estiver `aberto` ou `aguardando_solicitante`.
- Chamado `resolvido` ou `cancelado` não volta a nenhum outro status. Para continuar, o solicitante cria um novo com `chamado_origem_id` apontando para o anterior.
- Quando o solicitante comenta num chamado `aguardando_solicitante`, o status volta para `em_andamento` automaticamente.
- Ao atribuir um chamado `aberto`, o status passa para `em_andamento`.
- Prioridade `critica` dispara email imediato para todos os analistas ativos.
- Toda mudança de status, prioridade ou responsável grava um HistoricoStatus na mesma transação.

### Sobre Comentario
- Comentário com `visivel_para_solicitante = false` só aparece para analista e admin, também filtrado por RLS.
- Solicitante só cria comentário público.
- Comentário não é editado nem apagado depois de enviado.

### Sobre Anexo
- Até 10 MB por arquivo e 5 arquivos por chamado. Tipos: jpg, png, pdf, docx.
- O download usa URL assinada válida por 10 minutos, gerada só para quem pode ver o chamado.

### Sobre Evento
- Só é gravado pelo servidor ou por função do banco, nunca direto pelo navegador.
- Só analista e admin leem, e o Painel mostra apenas números agregados.
