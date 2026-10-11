# Estrutura de dados

*Cada entidade diz a qual lado pertence. Tabelas em `snake_case` no Postgres (Supabase), com PostGIS para localização.*

**Categorias** (enum `categoria`, usado em PerfilProfissional e Pedido): `eletrica`, `hidraulica`, `limpeza`, `pintura`, `pequenos_reparos`. Rótulos na tela: Elétrica, Hidráulica, Limpeza, Pintura, Pequenos reparos.

## Entidade: Usuario (base dos dois lados)
A conta de uma pessoa. Criada no primeiro login por telefone (o `id` é o mesmo do `auth.users` do Supabase).

**Campos:**
- `id` (uuid, único)
- `nome` (texto, obrigatório, 2 a 80 caracteres)
- `telefone` (texto, obrigatório, único, formato E.164 `+55...`, verificado por SMS)
- `email` (texto, obrigatório, usado só para notificações)
- `tipo` (enum: `morador` | `profissional`, obrigatório, imutável)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Tem um PerfilMorador se `tipo = morador`.
- Tem um PerfilProfissional se `tipo = profissional`.

---

## Entidade: PerfilMorador (lado da demanda)
Endereço padrão do morador, usado para pré-preencher pedidos.

**Campos:**
- `id` (uuid, único)
- `usuario_id` (uuid, obrigatório, único)
- `cep` (texto, obrigatório, 8 dígitos)
- `logradouro` (texto, obrigatório)
- `numero` (texto, obrigatório)
- `complemento` (texto, opcional)
- `bairro` (texto, obrigatório)
- `cidade` (texto, obrigatório)
- `localizacao` (geography point, obrigatório, gerado por geocodificação do endereço)

**Relacionamentos:**
- Pertence a um Usuario.
- Tem muitos Pedidos.

---

## Entidade: PerfilProfissional (lado da oferta)
A vitrine do profissional e os filtros que decidem quais pedidos ele vê.

**Campos:**
- `id` (uuid, único)
- `usuario_id` (uuid, obrigatório, único)
- `bio` (texto, opcional, até 400 caracteres)
- `foto_url` (texto, opcional)
- `fotos_trabalho` (array de texto, opcional, até 6 URLs)
- `categorias` (array de `categoria`, obrigatório, 1 a 3 itens)
- `cep_base` (texto, obrigatório)
- `bairro_base` (texto, obrigatório)
- `cidade` (texto, obrigatório)
- `localizacao` (geography point, obrigatório, centro do raio de atendimento)
- `raio_atendimento_km` (inteiro, obrigatório, 2 a 40, padrão 10)
- `disponivel` (booleano, obrigatório, padrão `true`)
- `media_avaliacao` (decimal 1 casa, calculado, nulo sem avaliação)
- `total_avaliacoes` (inteiro, calculado, padrão 0)
- `oculto` (booleano, calculado, padrão `false`)

**Relacionamentos:**
- Pertence a um Usuario.
- Tem muitas Propostas.
- Tem muitas Avaliacoes (como avaliado).

---

## Entidade: Pedido (lado da demanda)
Um serviço que o morador precisa resolver.

**Campos:**
- `id` (uuid, único)
- `morador_id` (uuid, obrigatório, referência a PerfilMorador)
- `categoria` (`categoria`, obrigatório)
- `titulo` (texto, obrigatório, 10 a 80 caracteres)
- `descricao` (texto, obrigatório, 20 a 600 caracteres)
- `urgente` (booleano, obrigatório, padrão `false`)
- `data_preferida` (data, opcional, hoje ou depois)
- `endereco_servico` (texto, obrigatório, pré-preenchido do PerfilMorador)
- `bairro` (texto, obrigatório)
- `localizacao` (geography point, obrigatório)
- `status` (enum: `aberto` | `com_propostas` | `em_andamento` | `concluido` | `cancelado` | `expirado`, obrigatório)
- `proposta_aceita_id` (uuid, opcional)
- `criado_em` (timestamp, obrigatório)
- `aceito_em` (timestamp, opcional)
- `concluido_em` (timestamp, opcional)

**Relacionamentos:**
- Pertence a um PerfilMorador.
- Tem muitas Propostas (no máximo 5).
- Tem no máximo uma Avaliacao.

---

## Entidade: Proposta (lado da oferta)
A resposta de um profissional a um pedido.

**Campos:**
- `id` (uuid, único)
- `pedido_id` (uuid, obrigatório)
- `profissional_id` (uuid, obrigatório, referência a PerfilProfissional)
- `valor_min` (inteiro em reais, obrigatório, maior que 0)
- `valor_max` (inteiro em reais, opcional, maior ou igual a `valor_min`)
- `prazo_execucao` (enum: `hoje` | `ate_2_dias` | `ate_7_dias` | `a_combinar`, obrigatório)
- `mensagem` (texto, obrigatório, 10 a 300 caracteres)
- `status` (enum: `enviada` | `aceita` | `recusada` | `cancelada`, obrigatório)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Pertence a um Pedido.
- Pertence a um PerfilProfissional.

---

## Entidade: Avaliacao (demanda avalia oferta)
A nota do morador para o profissional depois do serviço.

**Campos:**
- `id` (uuid, único)
- `pedido_id` (uuid, obrigatório, único)
- `avaliador_id` (uuid, obrigatório, referência a PerfilMorador)
- `avaliado_id` (uuid, obrigatório, referência a PerfilProfissional)
- `nota` (inteiro, obrigatório, 1 a 5)
- `comentario` (texto, opcional, até 300 caracteres)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Pertence a um Pedido.
- Pertence a um PerfilMorador (quem avalia) e a um PerfilProfissional (quem é avaliado).

---

## Regras de negócio

### Sobre Usuario
- Um telefone, uma conta, um tipo. Quem quiser usar os dois lados cria outra conta com outro telefone (fora do MVP resolver isso).
- O telefone de um usuário só é visível para a outra parte depois que uma proposta entre os dois é aceita.

### Sobre PerfilProfissional
- Profissional vê um Pedido somente se: `disponivel = true`, a categoria do pedido está em `categorias` e a distância entre `localizacao` do perfil e do pedido é menor ou igual a `raio_atendimento_km`.
- `media_avaliacao` e `total_avaliacoes` são recalculados por trigger a cada nova Avaliacao.
- `oculto = true` quando `total_avaliacoes >= 5` e `media_avaliacao < 2.0`. Perfil oculto não vê pedidos novos, não aparece na contagem de cobertura e não envia proposta. Com menos de 5 avaliações nunca oculta: uma nota ruim não derruba quem está começando.
- Profissional pode ter no máximo 10 propostas com status `enviada` ao mesmo tempo.

### Sobre Pedido
- Morador pode ter no máximo 3 pedidos em `aberto` ou `com_propostas` ao mesmo tempo.
- Transições de status permitidas: `aberto` → `com_propostas` (primeira proposta chega) → `em_andamento` (morador aceita) → `concluido` (morador marca). `aberto` e `com_propostas` podem ir para `cancelado` (morador cancela) ou `expirado` (72 horas sem proposta aceita). Nenhum status volta.
- Antes do aceite, o profissional vê só `bairro`, distância arredondada em km e a descrição. `endereco_servico` completo só aparece para o profissional da proposta aceita.
- Pedido para de receber propostas ao chegar a 5 propostas `enviada`.

### Sobre Proposta
- Um profissional envia no máximo uma proposta por pedido.
- Pedido tem no máximo uma proposta `aceita`. Ao aceitar uma, todas as outras do mesmo pedido viram `recusada` na mesma transação.
- Proposta `enviada` pode ser cancelada pelo profissional enquanto o pedido não estiver `em_andamento`.
- Morador só vê propostas dos próprios pedidos; profissional só vê as próprias propostas.

### Sobre Avaliacao
- Só existe para Pedido `concluido`, só pelo morador dono do pedido, uma por pedido.
- Pode ser feita até 14 dias depois de `concluido_em`. Não pode ser editada nem apagada pelo usuário.
