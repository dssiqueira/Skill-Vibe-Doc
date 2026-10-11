# Estrutura de dados

## Entidade: Usuario
Pessoa interna que acessa a ferramenta. Criada no primeiro login via SSO.

**Campos:**
- `id` (uuid, único, igual ao id do Supabase Auth)
- `nome` (texto, obrigatório)
- `email` (texto, obrigatório, domínio da empresa)
- `perfil` (enum, obrigatório): `backoffice` | `comercial`
- `ativo` (booleano, obrigatório, padrão `true`)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Comercial é responsável por muitos **Clientes**.
- Backoffice conduz muitos **Onboardings**.

---

## Entidade: Cliente
Empresa que acabou de contratar.

**Campos:**
- `id` (uuid, único)
- `nome_empresa` (texto, obrigatório)
- `cnpj` (texto, obrigatório, 14 dígitos sem máscara, único)
- `nome_contato` (texto, obrigatório)
- `email_contato` (texto, obrigatório; recebe o contrato e as credenciais)
- `telefone_contato` (texto, opcional)
- `plano_contratado` (enum, obrigatório): `essencial` | `profissional` | `enterprise` <!-- sugestão: confirmar -->
- `comercial_responsavel_id` (uuid, obrigatório, referência a Usuario com perfil `comercial`)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Tem muitos **Onboardings** ao longo do tempo, no máximo um ativo.

---

## Entidade: Onboarding
Uma passagem do cliente pela esteira, do formulário ao acesso liberado.

**Campos:**
- `id` (uuid, único)
- `cliente_id` (uuid, obrigatório)
- `status` (enum, obrigatório): `iniciado` | `contrato_enviado` | `contrato_assinado` | `acessos_criados` | `concluido` | `com_erro` | `cancelado`
- `etapa_atual_id` (uuid, opcional, referência a EtapaOnboarding; vazio quando concluído ou cancelado)
- `responsavel_id` (uuid, obrigatório, Usuario de backoffice que conduz)
- `iniciado_em` (timestamp, obrigatório)
- `contrato_assinado_em` (timestamp, opcional)
- `concluido_em` (timestamp, opcional)
- `cancelado_em` (timestamp, opcional)
- `motivo_cancelamento` (texto, obrigatório quando `status = cancelado`)

**Relacionamentos:**
- Pertence a um **Cliente**.
- Tem exatamente seis **EtapaOnboarding**, criadas junto com ele.
- Tem muitas entradas de **LogAuditoria**.

---

## Entidade: EtapaOnboarding
Um passo da esteira. A tabela de etapas é fixa e igual para todo onboarding.

**Campos:**
- `id` (uuid, único)
- `onboarding_id` (uuid, obrigatório)
- `ordem` (inteiro, obrigatório, 1 a 6)
- `nome` (enum, obrigatório): `envio_contrato` | `assinatura_contrato` | `acesso_sistema1` | `acesso_sistema2` | `acesso_sistema3` | `notificacao_conclusao`
- `modo` (enum, obrigatório): `automatica` | `aguarda_externo` | `manual`
- `status` (enum, obrigatório): `pendente` | `em_andamento` | `aguardando_humano` | `concluida` | `erro`
- `tentativas` (inteiro, obrigatório, padrão 0)
- `proxima_tentativa_em` (timestamp, opcional)
- `id_externo` (texto, opcional: id do envelope na D4Sign ou id do usuário criado no sistema interno; garante idempotência)
- `erro_mensagem` (texto, opcional: frase legível para a Fernanda)
- `erro_detalhe` (jsonb, opcional: resposta técnica da API, só no log)
- `executada_por` (enum `sistema` ou uuid de Usuario, opcional)
- `iniciada_em` (timestamp, opcional)
- `concluida_em` (timestamp, opcional)

**Relacionamentos:**
- Pertence a um **Onboarding**.
- Gera muitas entradas de **LogAuditoria**.

| ordem | nome | modo |
|---|---|---|
| 1 | envio_contrato | automatica |
| 2 | assinatura_contrato | aguarda_externo |
| 3 | acesso_sistema1 | automatica |
| 4 | acesso_sistema2 | automatica |
| 5 | acesso_sistema3 | manual |
| 6 | notificacao_conclusao | automatica |

---

## Entidade: LogAuditoria
Registro imutável de tudo que aconteceu. Só recebe inserção.

**Campos:**
- `id` (bigint, sequencial)
- `onboarding_id` (uuid, obrigatório)
- `etapa_id` (uuid, opcional; vazio em ações do onboarding como um todo)
- `acao` (texto, obrigatório, `snake_case`, mesmo nome do evento em `metricas.md`)
- `detalhes` (jsonb, obrigatório; sem senha nem token)
- `executado_por` (texto, obrigatório): `sistema` ou id do Usuario
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Pertence a um **Onboarding** e, opcionalmente, a uma **EtapaOnboarding**.

---

## Regras de negócio

### Sobre Cliente
- CNPJ é validado pelo dígito verificador antes de salvar. CNPJ que já tem onboarding ativo bloqueia o formulário e mostra o link para o onboarding existente.

### Sobre Onboarding
- Um cliente tem no máximo um onboarding com status diferente de `concluido` e `cancelado`.
- Nunca é apagado. Cancelar exige motivo e pode acontecer em qualquer status antes de `concluido`; cancelar não desfaz acessos já criados, gera tarefa no log para a Fernanda revogar à mão.
- `status` é derivado das etapas: qualquer etapa em `erro` leva o onboarding a `com_erro`; ao destravar, volta ao status da etapa atual.

### Sobre EtapaOnboarding
- Executadas estritamente em ordem. A etapa N só sai de `pendente` quando a N-1 está `concluida`.
- Etapa `automatica` com falha técnica (timeout, HTTP 5xx, limite de requisição) tenta de novo até 3 vezes, com espera de 1, 5 e 15 minutos. Falha de dado (HTTP 4xx, e-mail já cadastrado) vai direto para `erro`, sem nova tentativa.
- Toda chamada externa usa `id_externo` ou chave de idempotência: "Tentar novamente" nunca cria contrato ou conta em duplicidade.
- Etapa `manual` só é concluída por Usuario de backoffice, com todos os itens do checklist marcados.
- Etapa `aguarda_externo` (assinatura) só avança por webhook válido da D4Sign. Sem assinatura em 5 dias úteis, a etapa continua aguardando e a Fernanda recebe um aviso para cobrar o cliente; não vira erro.

### Sobre LogAuditoria
- Nenhuma ação, automática ou humana, acontece sem gravar uma linha antes de responder.
- Ninguém, nem o perfil backoffice, edita ou apaga linha de log (regra no banco, não só na tela).
