# Estrutura de dados

## Entidade: Usuario
Quem cria conta para salvar e exportar páginas.

**Campos:**
- `id` (uuid, único, o mesmo do Supabase Auth)
- `nome` (texto, obrigatório)
- `email` (texto, obrigatório, único)
- `plano` (enum `free | pro`, obrigatório, padrão `free`)
- `geracoes_no_mes` (inteiro, obrigatório, padrão 0, zera no dia 1 de cada mês)
- `stripe_customer_id` (texto, opcional, preenchido na primeira assinatura)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Tem muitas **Marcas**, muitos **Briefings** e muitas **LandingPages**.

---

## Entidade: Marca
A identidade visual de quem a página representa, guardada como um DESIGN.md válido. É a entrada visual do gerador.

**Campos:**
- `id` (uuid, único)
- `usuario_id` (uuid, obrigatório)
- `nome` (texto, obrigatório, ex.: "Fila Zero" ou "Mariana Nutri")
- `origem` (enum `importada | gerada | padrao`, obrigatório)
- `design_md` (texto, obrigatório, o arquivo completo, até 50 KB)
- `tokens` (json, obrigatório, frontmatter já interpretado: cores, tipografia, cantos, espaçamento, componentes)
- `tema_base` (enum `minimalista | bold | corporativo | colorido`, obrigatório só quando `origem = padrao`)
- `logo_url` (texto, opcional, caminho no storage)
- `versao` (inteiro, obrigatório, começa em 1 e sobe a cada edição)
- `hash_conteudo` (texto, obrigatório, sha256 do `design_md`)
- `criado_em`, `atualizado_em` (timestamp, obrigatórios)

**Relacionamentos:**
- Pertence a um **Usuario**.
- É usada por muitos **Briefings**.

---

## Entidade: Briefing
O que o usuário contou sobre o produto e a página que quer.

**Campos:**
- `id` (uuid, único)
- `usuario_id` (uuid, opcional: vazio enquanto a pessoa gera sem conta)
- `sessao_anonima_id` (texto, opcional, identifica geração sem conta)
- `marca_id` (uuid, obrigatório)
- `nome_produto` (texto, obrigatório, até 60 caracteres)
- `descricao_produto` (texto, obrigatório, 40 a 1.200 caracteres: o que faz, para quem, benefício principal)
- `publico_alvo` (texto, obrigatório, até 300 caracteres)
- `tom` (enum `profissional | descontraido | urgente | inspirador`, obrigatório)
- `objetivo_cta` (enum `lista_de_espera | contato | compra | cadastro`, obrigatório)
- `link_cta` (texto, obrigatório: URL, e-mail ou número de WhatsApp para onde o botão leva)
- `criado_em` (timestamp, obrigatório)

**Relacionamentos:**
- Pertence a um **Usuario** (ou a uma sessão anônima) e a uma **Marca**.
- Gera uma ou mais **LandingPages** (uma por geração).

---

## Entidade: LandingPage
O resultado de uma geração.

**Campos:**
- `id` (uuid, único)
- `briefing_id` (uuid, obrigatório)
- `usuario_id` (uuid, opcional, igual ao do briefing)
- `nome` (texto, obrigatório, padrão = `nome_produto` + data)
- `conteudo_gerado` (json, obrigatório, imutável: seções na ordem escolhida pela IA, cada uma com tipo e textos)
- `textos_editados` (json, opcional, sobrescritas por chave de seção e campo)
- `marca_versao` (inteiro, obrigatório, versão da Marca usada na geração)
- `marca_hash` (texto, obrigatório, `hash_conteudo` da Marca no momento da geração)
- `html_exportado` (texto, opcional, último HTML exportado)
- `status` (enum `gerando | pronta | falhou | exportada | arquivada`, obrigatório)
- `custo_estimado_centavos` (inteiro, obrigatório, custo da chamada de IA em centavos de real)
- `tempo_geracao_ms` (inteiro, opcional)
- `gerado_em`, `exportado_em`, `arquivado_em` (timestamp, os dois últimos opcionais)

**Relacionamentos:**
- Pertence a um **Briefing** e a um **Usuario**.

---

## Regras de negócio

### Sobre Usuario
- Free: no máximo 3 gerações por mês. Pro: ilimitado com teto de uso justo de 100 gerações por mês; acima disso, bloqueia e avisa por e-mail.
- Cada geração consome 1 crédito no momento em que a IA responde com sucesso. Geração que falhou não consome crédito. Editar texto não consome.

### Sobre Marca
- Só é salva se o DESIGN.md passar no lint do padrão com 0 erros (contraste mínimo de 4,5:1 incluso). Warnings são mostrados mas não bloqueiam.
- Precisa ter pelo menos os tokens `primary`, `on-primary`, `surface`, `on-surface` e uma tipografia de corpo. Se faltar, o produto completa a partir do tema padrão e avisa quais tokens foram completados.
- Editar a Marca cria nova `versao`; páginas já geradas continuam com a versão que usaram até o usuário pedir para reaplicar.
- Todo usuário tem uma Marca de origem `padrao` criada no cadastro. Ela não pode ser apagada.

### Sobre Briefing
- Sem conta: gera 1 página por sessão anônima (contando para o limite por IP de 3 por dia). Para salvar ou exportar, precisa criar conta; o briefing e a página migram para o usuário.

### Sobre LandingPage
- `conteudo_gerado` é imutável. Edição só grava em `textos_editados`.
- "Gerar novamente" cria uma nova LandingPage e consome outro crédito; a anterior continua no histórico.
- Não pode ser apagada, só arquivada. Arquivada some do histórico principal e aparece no filtro "Arquivadas".
- Exportar exige conta e `status` em `pronta` ou `exportada`. Blocos de prova social ainda com placeholder geram aviso antes de exportar.
