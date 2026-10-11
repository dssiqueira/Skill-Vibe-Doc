# Fluxos e telas

*Aqui fica o que existe no produto e por onde a pessoa anda. Cor, fonte e estilo ficam no DESIGN.md. Os dois lados têm áreas separadas; depois do login, o `tipo` do Usuario decide qual área abre.*

## Princípios de experiência

1. **Mostrar oferta antes de pedir cadastro.** A Cláudia vê quantos profissionais atendem o bairro dela antes de digitar o telefone.
2. **Uma ação principal por tela**, sempre no rodapé e alcançável com o polegar.
3. **Reputação em todo lugar.** Onde aparece um profissional, aparecem nota e número de avaliações.
4. **Pedido publicado em até 2 minutos; proposta enviada em até 1 minuto.**
5. **Status sempre visível.** O morador sabe em que pé está cada pedido sem abrir o pedido.

## Mapa de telas

**Comum**
- Início público: consultar cobertura por CEP e categoria, sem login.
- Entrar: login e cadastro por telefone com código SMS.

**Morador**
- Início do morador: atalhos de categoria e lista dos meus pedidos com status.
- Novo pedido: descrever e publicar o serviço.
- Detalhe do pedido: status, propostas recebidas, contato após aceite, concluir e avaliar.
- Perfil do profissional: reputação, bio e fotos de trabalho de quem mandou proposta.
- Avaliar: nota e comentário depois do serviço.

**Profissional**
- Cadastro do profissional: 3 passos (categorias, área de atendimento, apresentação).
- Pedidos na região: disponibilidade e lista de pedidos que ele pode atender.
- Detalhe do pedido e envio de proposta.
- Minhas propostas: o que foi enviado, aceito ou recusado, e o contato após aceite.
- Meu perfil: editar dados e ver as próprias avaliações.

---

## Tela: Início público

**Objetivo:** responder "tem alguém que atende aqui?" em 10 segundos.

### Hierarquia do conteúdo
1. Frase de valor: "Profissionais avaliados por vizinhos, perto de você."
2. Campo de CEP.
3. Grade com as 5 categorias.
4. Resultado: "7 profissionais de Hidráulica atendem o Cambuí" e as 3 maiores notas (foto, primeiro nome, nota).
5. Link discreto: "Sou profissional e quero receber pedidos".

### Ações e interações
- Digitar CEP com 8 dígitos e escolher categoria → busca a contagem e mostra o resultado na mesma tela.
- "Pedir orçamento" (aparece com 1 ou mais profissionais) → Entrar, e depois Novo pedido com CEP e categoria já preenchidos.
- Resultado com 0 profissionais → mensagem "Ainda não temos profissionais de Hidráulica aqui." sem botão de pedido, com o link "Conhece um bom profissional? Indique o Resolve Aí" (compartilha o link de cadastro pelo WhatsApp). A consulta com 0 fica registrada para guiar o recrutamento.
- "Sou profissional" → Entrar com tipo `profissional` pré-selecionado.

---

## Tela: Entrar

**Objetivo:** criar conta ou entrar sem senha.

### Hierarquia do conteúdo
1. Campo de telefone com DDD.
2. Escolha do lado ("Preciso de um serviço" ou "Quero oferecer serviços"), só no primeiro acesso.
3. Campo do código de 6 dígitos (aparece após enviar).
4. No primeiro acesso: nome e email.

### Ações e interações
- "Receber código" → envia SMS, mostra campo do código e contador de 60 segundos para reenviar.
- Código correto → conta existente vai para o início do seu lado; conta nova pede nome e email e segue.
- Código errado 5 vezes → bloqueio de 15 minutos com aviso.

---

## Tela: Início do morador

**Objetivo:** abrir um pedido novo ou acompanhar os que estão em aberto.

### Hierarquia do conteúdo
1. Pedidos ativos (`aberto`, `com_propostas`, `em_andamento`) com título, selo de status e número de propostas.
2. Grade de categorias: tocar abre Novo pedido com a categoria escolhida.
3. Pedidos encerrados (`concluido`, `cancelado`, `expirado`), recolhidos em "Ver anteriores".

### Ações e interações
- Toque em um pedido → Detalhe do pedido.
- Toque em categoria → Novo pedido.
- Pedido concluído sem avaliação mostra o atalho "Avaliar" no próprio card.

---

## Tela: Novo pedido

**Objetivo:** publicar o pedido em até 2 minutos.

### Hierarquia do conteúdo
1. Categoria (já marcada se veio de atalho; troca com um toque).
2. Título: "O que precisa ser feito, em uma frase".
3. Descrição: "Conte detalhes: o que aconteceu, onde fica, tamanho".
4. Interruptor "É urgente?" com explicação: "Profissionais veem seu pedido primeiro".
5. Data preferida (opcional), com atalhos "Hoje", "Amanhã", "Esta semana".
6. Endereço do serviço, pré-preenchido do perfil; "Usar outro endereço" abre CEP, número e complemento.
7. Botão fixo "Publicar pedido".

### Ações e interações
- No primeiro pedido, sem PerfilMorador: o endereço é obrigatório e vira o endereço padrão.
- "Publicar pedido" → valida, geocodifica o endereço, cria o Pedido em `aberto`, notifica profissionais elegíveis e abre o Detalhe do pedido com "Pedido publicado. Avisamos 7 profissionais."
- Sair com o formulário preenchido → pergunta "Descartar pedido?".

---

## Tela: Detalhe do pedido (morador)

**Objetivo:** comparar propostas, aceitar uma e fechar o ciclo.

### Hierarquia do conteúdo
1. Título, selo de status, selo "Urgente" se houver, tempo desde a publicação.
2. Conforme o status:
   - `aberto`: "Avisamos 7 profissionais. Propostas costumam chegar em até 2 horas."
   - `com_propostas`: lista de propostas (foto, nome, nota e avaliações, faixa de valor, prazo, mensagem em 3 linhas), na ordem de chegada.
   - `em_andamento`: card do profissional escolhido com "Chamar no WhatsApp", "Ligar" e "Marcar como concluído".
   - `concluido`: avaliação feita ou atalho "Avaliar".
3. Descrição e endereço do pedido.
4. "Cancelar pedido", no fim da tela.

### Ações e interações
- "Ver perfil completo" → Perfil do profissional.
- "Aceitar proposta" → modal "Aceitar a proposta do João por R$ 120 a R$ 180? As outras propostas serão recusadas." → confirma → status `em_andamento`, contato liberado, profissional notificado.
- "Chamar no WhatsApp" → abre `wa.me` com mensagem pronta: "Oi, João! Aceitei sua proposta no Resolve Aí para: Torneira da cozinha pingando."
- "Marcar como concluído" → status `concluido` e vai para Avaliar.
- "Cancelar pedido" → modal de confirmação com `button-danger` → status `cancelado`, profissionais com proposta são avisados.

---

## Tela: Perfil do profissional (visto pelo morador)

**Objetivo:** dar segurança para escolher.

### Hierarquia do conteúdo
1. Foto, nome, categorias, nota média e total de avaliações, "No Resolve Aí desde março de 2026".
2. Últimas 10 avaliações com nota, comentário, primeiro nome do morador e mês.
3. Bio.
4. Fotos de trabalho (até 6, em grade; toque amplia).
5. Botão fixo "Aceitar proposta" quando veio de uma proposta.

### Ações e interações
- Aceitar a partir daqui segue o mesmo modal do Detalhe do pedido.
- Telefone nunca aparece nesta tela antes do aceite.

---

## Tela: Avaliar

**Objetivo:** registrar a nota em 15 segundos.

### Hierarquia do conteúdo
1. "Como foi o serviço do João?" com foto.
2. 5 estrelas grandes.
3. Comentário opcional.
4. Botão "Enviar avaliação".

### Ações e interações
- Nota obrigatória; comentário não.
- Enviar → cria Avaliacao, recalcula média do profissional, volta ao Início do morador com "Obrigado. Sua avaliação ajuda outros vizinhos."

---

## Tela: Cadastro do profissional

**Objetivo:** do código SMS ao primeiro pedido visível em até 3 minutos.

### Hierarquia do conteúdo
1. Passo 1 de 3, **O que você faz:** até 3 categorias.
2. Passo 2 de 3, **Onde você atende:** CEP base e raio (2, 5, 10, 20 ou 40 km), com o bairro e a contagem de pedidos dos últimos 30 dias nesse raio.
3. Passo 3 de 3, **Sua apresentação:** foto de perfil e bio, os dois opcionais, com "Pular por agora".

### Ações e interações
- Cada passo tem só "Continuar"; "Voltar" no topo.
- Concluir → cria PerfilProfissional com `disponivel = true` e abre Pedidos na região.
- Sem foto, Pedidos na região mostra um lembrete: "Perfis com foto recebem mais aceites."

---

## Tela: Pedidos na região (início do profissional)

**Objetivo:** ver em segundos se há trabalho para ele agora.

### Hierarquia do conteúdo
1. Interruptor de disponibilidade: "Disponível para pedidos" ou "Indisponível".
2. Filtro por categoria (só as dele), padrão "Todas".
3. Lista de pedidos elegíveis: urgentes primeiro, depois mais recentes. Cada card: título, categoria, bairro, distância, tempo desde a abertura, selo "Urgente", quantas propostas já tem ("2 de 5 propostas").
4. Pedidos em que ele já mandou proposta ficam fora desta lista.

### Ações e interações
- Toque no card → Detalhe do pedido (profissional).
- Desligar disponibilidade → lista some, aparece "Você não recebe pedidos novos enquanto estiver indisponível." e os emails de pedido novo param.
- Puxar para baixo → atualiza a lista.

---

## Tela: Detalhe do pedido e envio de proposta (profissional)

**Objetivo:** decidir e mandar proposta em até 1 minuto.

### Hierarquia do conteúdo
1. Título, categoria, selo "Urgente", data preferida.
2. Descrição completa.
3. Bairro e distância ("Cambuí, a 4 km"). Endereço completo só após aceite.
4. Formulário: valor mínimo, valor máximo (opcional), prazo (Hoje, Até 2 dias, Até 7 dias, A combinar), mensagem com sugestão editável.
5. Botão fixo "Enviar proposta".

### Ações e interações
- "Enviar proposta" → cria Proposta `enviada`, pedido vira `com_propostas` se era `aberto`, morador é notificado, volta para Pedidos na região com "Proposta enviada."
- Pedido que chegou a 5 propostas ou foi cancelado enquanto ele preenchia → aviso "Esse pedido não recebe mais propostas" e o texto digitado é descartado.

---

## Tela: Minhas propostas

**Objetivo:** saber o que deu certo e falar com o cliente.

### Hierarquia do conteúdo
1. Abas: "Aguardando", "Aceitas", "Encerradas" (recusadas, canceladas, pedidos expirados).
2. Card com título do pedido, bairro, valor proposto e status.
3. Em "Aceitas": nome do morador, endereço completo, "Chamar no WhatsApp" e "Ligar".

### Ações e interações
- "Cancelar proposta" em propostas aguardando → modal → status `cancelada`.
- Proposta aceita gera email com o contato do morador.

---

## Tela: Meu perfil (profissional)

**Objetivo:** manter a vitrine atualizada e acompanhar a reputação.

### Hierarquia do conteúdo
1. Nota média, total de avaliações e as últimas avaliações recebidas.
2. Foto, bio e fotos de trabalho (adicionar ou remover, até 6).
3. Categorias e raio de atendimento.
4. Nome, telefone (só leitura) e email.
5. "Sair".

### Ações e interações
- Editar qualquer bloco salva na hora, com confirmação em texto.
- Trocar raio ou categorias atualiza Pedidos na região na próxima abertura.

---

## Fluxo principal: Cláudia pede um serviço

1. Abre o Início público, digita o CEP e toca em "Hidráulica". Vê "7 profissionais atendem o Cambuí".
2. Toca em "Pedir orçamento", informa o telefone, recebe o SMS, digita o código, nome e email.
3. Em Novo pedido, a categoria já está marcada. Escreve título e descrição, liga "É urgente?", confirma o endereço e publica.
4. Recebe email "Nova proposta para: Torneira da cozinha pingando". Abre o Detalhe do pedido e compara as propostas.
5. Abre o perfil do Seu João, lê as avaliações e aceita a proposta.
6. Toca em "Chamar no WhatsApp" e combina o horário.
7. Depois do serviço, toca em "Marcar como concluído" e avalia com 5 estrelas.

**Tempo esperado:** passos 1 a 3 em até 3 minutos no primeiro uso, até 2 minutos nos seguintes. Primeira proposta em até 2 horas para pedido urgente.

## Fluxo principal: Seu João entra e responde um pedido

1. Clica em "Sou profissional" no Início público, informa telefone e código, nome e email.
2. Faz o Cadastro do profissional em 3 passos (Elétrica, raio de 20 km, pula a foto).
3. Cai em Pedidos na região com o interruptor ligado.
4. Recebe email "Pedido urgente de Elétrica a 6 km". Abre, lê a descrição, preenche R$ 120 a R$ 180, prazo "Hoje", e envia.
5. Recebe email "Sua proposta foi aceita" com o telefone da Cláudia. Em Minhas propostas, toca em "Chamar no WhatsApp".

**Tempo esperado:** passos 1 e 2 em até 3 minutos; passo 4 em até 1 minuto.

## Fluxo secundário: pedido sem resposta

1. Pedido em `aberto` há 24 horas sem proposta → email ao morador: "Ainda sem propostas. Quer aumentar a chance? Adicione detalhes ou marque como urgente." O botão leva ao Detalhe do pedido.
2. Pedido sem proposta aceita em 72 horas → status `expirado`, email ao morador com atalho "Publicar de novo" (abre Novo pedido com os mesmos dados) e aviso aos profissionais com proposta enviada.

## Estados

- **Vazio:**
  - Início do morador sem pedidos: ícone das categorias e "Do que sua casa precisa hoje?" com a grade de categorias.
  - Pedido `aberto` sem propostas: "Avisamos 7 profissionais. Propostas costumam chegar em até 2 horas."
  - Pedidos na região sem pedidos: "Nenhum pedido no seu raio agora. Avisamos por email quando chegar." e atalho para aumentar o raio.
  - Minhas propostas sem propostas: "Você ainda não mandou propostas." com atalho para Pedidos na região.
  - Perfil sem avaliação: "Novo no Resolve Aí".
- **Carregando:** esqueleto dos cards na forma final (3 cards); botão de ação com "Enviando..." e bloqueado.
- **Erro:**
  - Campo inválido: mensagem embaixo do campo dizendo como corrigir; o botão principal mostra o primeiro erro.
  - CEP não encontrado: "Não achamos esse CEP. Confira os números."
  - Falha ao salvar: toast "Não deu para enviar. Seus dados continuam aqui." com "Tentar de novo"; o formulário nunca é limpo.
  - Proposta aceita por outro caminho (pedido já `em_andamento`): "Esse pedido já foi fechado com outro profissional."
- **Sem conexão:** faixa fixa no topo "Sem internet. Mostrando a última versão." Listas mostram o último conteúdo carregado; botões de publicar, enviar e aceitar ficam desabilitados com o motivo. Rascunho de pedido e de proposta fica salvo no aparelho.
- **Sem permissão:** morador que abre link de área do profissional (ou o contrário) vai para o próprio início com "Essa área é para profissionais." Pedido de outro morador retorna "Pedido não encontrado". Profissional oculto vê "Seu perfil está pausado por avaliações baixas. Fale com o suporte." e o email de suporte.
