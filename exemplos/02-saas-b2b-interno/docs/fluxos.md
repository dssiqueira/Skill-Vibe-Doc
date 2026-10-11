# Fluxos e telas

*Aqui fica o que existe no produto e por onde a pessoa anda. Cor, fonte e estilo ficam no DESIGN.md.*

São duas experiências diferentes no mesmo sistema. O solicitante vê poucas telas, com pouco texto e uma ação clara. O analista vê uma ferramenta densa, feita para ficar aberta o dia inteiro. O perfil do usuário decide qual navegação aparece.

## Princípios de experiência
1. Abrir um chamado leva menos de 3 minutos e no máximo 5 campos.
2. O solicitante nunca precisa perguntar o status: ele está na lista, no detalhe e no email.
3. O analista muda status, prioridade ou responsável em até 2 cliques, sem sair da tela de detalhe.
4. Crítico aparece primeiro, sempre. A ordem da fila não depende de filtro.
5. Ação destrutiva (cancelar chamado, desativar usuário) pede confirmação. Ação reversível não pede.

## Mapa de telas

**Comum**
- Login: entrar com a conta Microsoft corporativa.

**Solicitante**
- Meus chamados: ver os próprios pedidos e o status de cada um.
- Novo chamado: abrir um pedido em menos de 3 minutos.
- Detalhe do chamado (solicitante): acompanhar, responder e cancelar.

**Analista e admin**
- Fila: ver tudo que está pendente, em ordem de urgência.
- Detalhe do chamado (analista): agir sobre o chamado e conversar com o solicitante e com o time.
- Novo chamado em nome de: registrar pedido que chegou por corredor ou telefone.
- Painel: ver volume, tempo de resolução e carga por analista.

**Admin**
- Usuários: ajustar perfil e desativar acesso.

Navegação: barra lateral fixa à esquerda, com ícone e rótulo, sem submenu. Solicitante vê "Meus chamados" e "Novo chamado". Analista vê "Fila", "Novo chamado" e "Painel". Admin vê também "Usuários". Nome, perfil e "Sair" ficam no rodapé da barra.

---

## Tela: Login

**Objetivo:** entrar sem criar senha.

### Hierarquia do conteúdo
1. Nome do produto e uma frase: "Pedidos de TI em um só lugar".
2. Botão "Entrar com a conta Microsoft".
3. Aviso: "Acesso apenas pela rede interna ou VPN".

### Ações e interações
- Entrar com a conta Microsoft → SSO do Entra ID → volta para "Meus chamados" (solicitante) ou "Fila" (analista e admin).
- Se a pessoa tentou abrir um link de chamado antes do login, volta para esse chamado depois de entrar.

---

## Tela: Meus chamados

**Objetivo:** Marcos saber, em 5 segundos, como estão os pedidos dele.

### Hierarquia do conteúdo
1. Botão "Novo chamado", no topo, em destaque. É a única ação principal da tela.
2. Lista de chamados em andamento (`aberto`, `em_andamento`, `aguardando_solicitante`), mais recente em cima. Cada linha: número, título, categoria, selo de status, responsável (ou "Ainda não atribuído") e "atualizado há X".
3. Chamados `aguardando_solicitante` ganham a frase "O TI precisa de uma resposta sua" na linha.
4. Aba "Encerrados" com resolvidos e cancelados dos últimos 90 dias.

### Ações e interações
- Clicar na linha → Detalhe do chamado (solicitante).
- Novo chamado → tela Novo chamado.

---

## Tela: Novo chamado

**Objetivo:** registrar o pedido em menos de 3 minutos, com linguagem de quem não é técnico.

### Hierarquia do conteúdo
1. Título: "O que você precisa?" (obrigatório, até 120 caracteres).
2. Categoria, em 4 opções clicáveis com uma linha de explicação cada:
   - Acesso: "Senha, permissão de pasta ou sistema".
   - Suporte: "Algo parou de funcionar".
   - Equipamento: "Notebook, monitor, mouse, headset".
   - Outro: "Não sei onde encaixar".
3. Descrição (obrigatória, texto longo), com dica: "Conte o que aconteceu e desde quando".
4. Prioridade, já marcada como Média, com a descrição de cada nível:
   - Baixa: "Pode esperar alguns dias".
   - Média: "Atrapalha, mas consigo trabalhar".
   - Alta: "Não consigo fazer parte do meu trabalho".
   - Crítica: "Ninguém do meu time consegue trabalhar" (ao escolher, aparece o aviso "Todo o TI será avisado agora").
5. Anexo opcional: arrastar ou escolher arquivo (jpg, png, pdf, docx, até 10 MB, até 5 arquivos).
6. Botão "Abrir chamado".

### Ações e interações
- Abrir chamado → valida campos obrigatórios → cria o chamado → vai para o Detalhe com a mensagem "Chamado #1042 aberto. Você recebe um email a cada atualização."
- Sair da tela com texto preenchido → pergunta "Descartar o chamado?".
- Anexo acima do limite ou de tipo não aceito → erro no próprio campo, sem apagar o resto do formulário.

---

## Tela: Detalhe do chamado (solicitante)

**Objetivo:** saber em que pé está e responder quando o TI pedir.

### Hierarquia do conteúdo
1. Número, título e selo de status.
2. Quando `aguardando_solicitante`: faixa no topo "O TI precisa de uma resposta sua", com foco no campo de resposta.
3. Linha do tempo: abertura, mudanças de status e comentários públicos, em ordem cronológica. Comentários internos nunca aparecem.
4. Campo "Responder" com anexo e botão "Enviar".
5. Dados do chamado: categoria, prioridade, responsável, aberto em.
6. Botão "Cancelar chamado", discreto, só nos status `aberto` e `aguardando_solicitante`.
7. Em chamado `resolvido`: botão "Ainda não resolveu? Abrir novo chamado", que abre o formulário com título e categoria copiados e o vínculo ao anterior.

### Ações e interações
- Enviar resposta → comentário público; se o chamado estava `aguardando_solicitante`, volta para `em_andamento`.
- Cancelar chamado → confirmação "Cancelar o chamado #1042? Isso não pode ser desfeito." → status `cancelado`.

---

## Tela: Fila

**Objetivo:** Rafael ver o que está pendente e decidir o próximo atendimento em 10 segundos.

### Hierarquia do conteúdo
1. Contadores no topo: não atribuídos, meus em andamento, críticos abertos.
2. Filtros rápidos: Todos | Não atribuídos | Meus chamados | Aguardando solicitante, mais filtro por categoria e busca por texto (número, título, nome do solicitante).
3. Lista em tabela densa, ordenada sempre por: críticos primeiro, depois alta, depois data de abertura (mais antigo em cima). Colunas: número, título, solicitante e departamento, categoria, prioridade, status, responsável, tempo aberto.
4. Linha de chamado crítico com marcação de prioridade crítica, que não some com nenhum filtro de status ativo.

### Ações e interações
- Clicar na linha → Detalhe do chamado (analista).
- "Atribuir a mim" na própria linha, ao passar o mouse → atribui e muda para `em_andamento`, sem sair da fila.
- Chamado novo aparece na fila sem recarregar (atualização em tempo real) e o contador pisca uma vez.
- Atalhos: `/` foca a busca, `j` e `k` andam entre linhas, `Enter` abre.

---

## Tela: Detalhe do chamado (analista)

**Objetivo:** resolver o chamado sem trocar de tela.

### Hierarquia do conteúdo
1. Número, título, selo de status e prioridade.
2. Painel de ação à direita, sempre visível: Status, Prioridade e Responsável como seletores que salvam ao escolher.
3. Descrição original e anexos.
4. Linha do tempo completa: comentários públicos, comentários internos (visualmente distintos e marcados "Interno") e mudanças do HistoricoStatus.
5. Campo de comentário com alternador Público | Interno (padrão Público), anexo e botão "Enviar".
6. Dados do solicitante: nome, departamento, email e quantos chamados abertos ele tem.
7. Se houver `chamado_origem_id`: link "Continua o chamado #1031".

### Ações e interações
- Mudar Status, Prioridade ou Responsável → salva na hora, registra no histórico, mostra "Salvo" por 2 segundos. Sem confirmação.
- Mudar para `resolvido` → pede um comentário público de fechamento (obrigatório, pode ser curto) e envia email ao solicitante.
- Mudar para `aguardando_solicitante` → pede um comentário público com a pergunta.
- Mudar para `cancelado` → confirmação.
- Enviar comentário Interno → só o TI vê, sem email para o solicitante.

---

## Tela: Novo chamado em nome de

**Objetivo:** registrar em menos de 1 minuto o pedido que chegou pessoalmente.

### Hierarquia do conteúdo
1. Campo "Solicitante", com busca por nome ou email (obrigatório).
2. Os mesmos campos do Novo chamado, sem os textos de ajuda.
3. Opção "Já resolvi" que cria o chamado direto como `resolvido`, com comentário de fechamento.

### Ações e interações
- Abrir chamado → cria com `aberto_por_id` do analista e `solicitante_id` do colaborador; o solicitante recebe email de abertura.

---

## Tela: Painel

**Objetivo:** mostrar ao time e à coordenação se a fila está saudável.

Os números vêm de Chamado, HistoricoStatus e Evento, sempre agregados; o Painel nunca lista ações de uma pessoa específica além da carga por analista.

### Hierarquia do conteúdo
1. Período (últimos 7, 30 ou 90 dias).
2. Chamados abertos no período e tempo mediano de resolução por categoria.
3. Taxa de resolução sem idas e vindas e taxa de cancelamento.
4. Chamados resolvidos e em andamento por analista.
5. Percentual de chamados abertos como crítico e quantos tiveram a prioridade rebaixada.

### Ações e interações
- Trocar período → recalcula tudo.
- Clicar num número → abre a Fila com o filtro correspondente.

---

## Tela: Usuários (admin)

**Objetivo:** corrigir perfil e tirar acesso de quem saiu.

### Hierarquia do conteúdo
1. Busca por nome ou email.
2. Tabela: nome, email, departamento, perfil, ativo, último acesso.

### Ações e interações
- Mudar perfil → salva na hora e passa a valer no próximo carregamento da pessoa.
- Desativar → confirmação → a pessoa perde o acesso; os chamados dela continuam.

---

## Fluxo principal: Marcos abre um chamado
1. Marcos clica em "Novo chamado" na barra lateral ou em Meus chamados.
2. Escreve o título, escolhe a categoria e descreve o problema.
3. Mantém ou ajusta a prioridade lendo a descrição de cada nível.
4. Anexa um print, se tiver.
5. Clica em "Abrir chamado" e cai no detalhe com a confirmação.

**Tempo esperado:** menos de 3 minutos.

## Fluxo principal: Rafael atende a fila
1. Rafael abre a Fila; críticos e altos estão no topo.
2. Clica em "Atribuir a mim" no primeiro não atribuído.
3. Abre o detalhe, lê, comenta internamente se precisar de um colega.
4. Se falta informação, muda para `aguardando_solicitante` com a pergunta; Marcos recebe email.
5. Resolve e muda para `resolvido` com comentário de fechamento; Marcos recebe email.

**Tempo esperado:** atribuir e mudar status em até 2 cliques cada.

## Fluxo: pedido feito no corredor
1. Rafael volta à mesa e clica em "Novo chamado" (abre a versão "em nome de").
2. Busca o colaborador, preenche título e categoria.
3. Marca "Já resolvi" se resolveu na hora.

**Tempo esperado:** menos de 1 minuto.

## Fluxo: chamado resolvido que voltou a dar problema
1. Marcos abre o chamado resolvido e clica em "Ainda não resolveu? Abrir novo chamado".
2. O formulário vem com título e categoria copiados e o vínculo ao anterior.
3. Marcos descreve o que voltou a acontecer e envia.

---

## Estados
- **Vazio (Meus chamados):** "Você ainda não abriu nenhum chamado. Precisa de algo do TI?" com o botão "Novo chamado".
- **Vazio (Fila, filtro sem resultado):** "Nenhum chamado neste filtro." com link "Ver todos".
- **Vazio (Fila sem pendências):** "Fila zerada." sem ilustração.
- **Carregando:** esqueleto das linhas da lista ou da tabela; nunca tela branca. Ações do painel do analista mostram indicador no próprio seletor.
- **Erro ao salvar:** mensagem no ponto da ação ("Não foi possível mudar o status. Tente de novo."), valor volta ao anterior, nada do que foi digitado se perde.
- **Erro no envio do formulário:** campos preenchidos continuam lá; o erro aparece no campo com problema.
- **Sem conexão ou fora da VPN:** faixa no topo "Sem conexão com a rede da empresa. Conecte-se à VPN." Formulário mantém o rascunho no navegador e envia quando a conexão volta, com aviso.
- **Sem permissão:** solicitante que abre link de chamado de outra pessoa vê "Este chamado não é seu ou não existe." com link para Meus chamados. Nunca revela título nem dono.
- **Usuário desativado:** depois do SSO, "Seu acesso ao Balcão TI está desativado. Fale com o TI pelo ramal 4000."
