# Fluxos e telas

*Aqui fica o que existe no produto e por onde a pessoa anda. Cor, fonte e estilo ficam no DESIGN.md.*

## Princípios de experiência

1. **O que travou aparece primeiro.** Onboarding com erro ou esperando a Fernanda fica no topo do painel, antes de qualquer outra coisa.
2. **Destravar sem sair da tela.** Toda etapa com erro mostra a mensagem e a ação de destravar no próprio bloco.
3. **A automação mostra o que fez.** Cada etapa diz quem executou (Automático ou o nome da pessoa), quando, e o id gerado no sistema externo.
4. **Nada irreversível sem confirmação.** Iniciar onboarding (manda contrato ao cliente) e cancelar pedem confirmação; o resto é desfazível ou idempotente.
5. **Comercial vê, não mexe.** O perfil comercial não enxerga nenhum botão de ação.

## Mapa de telas

- **Login**: entrar com a conta Google da empresa.
- **Painel**: todos os onboardings ativos agrupados por status, com o que precisa de atenção em cima.
- **Novo onboarding**: formulário que cria Cliente e Onboarding e dispara a esteira.
- **Detalhe do onboarding**: linha do tempo das seis etapas, dados do cliente, ações e log de auditoria.
- **Histórico**: onboardings concluídos e cancelados, com busca.

---

## Tela: Login

**Objetivo:** entrar sem senha nova.

### Hierarquia do conteúdo
1. Nome do produto.
2. Botão "Entrar com Google".

### Ações e interações
- "Entrar com Google" → SSO do Google Workspace. Conta fora do domínio da empresa vê "Use seu e-mail da empresa". Primeiro login cria Usuario com perfil `comercial`; perfil `backoffice` é concedido por outro backoffice (ver `integracoes.md`).
- Sessão dura 30 dias no mesmo navegador, para o Bruno não logar toda vez.

---

## Tela: Painel

**Objetivo:** em 5 segundos, saber o que precisa de mim agora.

### Hierarquia do conteúdo
1. Faixa "Precisa de você": contagem e cards de onboardings em `com_erro` ou com etapa manual em `aguardando_humano`. Só aparece se houver algum.
2. Colunas por status: Contrato enviado, Aguardando assinatura, Criando acessos, Etapa manual. Cada card mostra empresa, plano, comercial responsável, etapa atual com badge e tempo desde o início.
3. Contador: "X concluídos nesta semana" e mediana de tempo interno da semana.
4. Botão "+ Novo onboarding" (só backoffice).

### Ações e interações
- Clicar no card → Detalhe do onboarding.
- Filtro "Só os meus": para backoffice, filtra por `responsavel_id`; para comercial, filtra por `comercial_responsavel_id` e já vem ligado.
- Painel atualiza sozinho via Realtime quando uma etapa muda de status, sem recarregar a página.
- Não aparece: onboardings concluídos há mais de 7 dias (vão para o Histórico) e qualquer valor de contrato.

---

## Tela: Novo onboarding

**Objetivo:** iniciar um onboarding em menos de 3 minutos sem digitar nada duas vezes.

### Hierarquia do conteúdo
1. Dados da empresa: nome da empresa, CNPJ.
2. Contato que assina e recebe acesso: nome, e-mail, telefone (opcional).
3. Plano contratado (select) e comercial responsável (select com Usuarios de perfil comercial ativos).
4. Botão "Iniciar onboarding".

### Ações e interações
- CNPJ é validado ao sair do campo (dígito verificador). CNPJ com onboarding ativo mostra "Este cliente já tem um onboarding em andamento" com link.
- E-mail é validado no formato e confirmado em um segundo campo, porque é para onde vai o contrato.
- "Iniciar onboarding" → modal de confirmação com resumo ("O contrato do plano Profissional será enviado para ana@cliente.com.br") → ao confirmar, cria Cliente, Onboarding e as seis etapas, dispara a etapa 1 e redireciona para o Detalhe.
- O botão fica desabilitado depois do clique até a resposta, para não disparar dois contratos.

---

## Tela: Detalhe do onboarding

**Objetivo:** ver exatamente onde o cliente está e destravar o que travou.

### Hierarquia do conteúdo
1. Cabeçalho: nome da empresa, status geral com badge, tempo desde o início, responsável no backoffice.
2. Linha do tempo vertical com as seis etapas, na ordem. Cada uma com ícone de estado, nome, quem executou, timestamp e id externo quando houver.
   - Etapa com `erro`: mensagem legível, número de tentativas e botão "Tentar novamente".
   - Etapa manual em `aguardando_humano`: checklist do Sistema 3 (criar usuário com o e-mail X, aplicar perfil do plano Y, copiar o login gerado) e botão "Marcar como feito", habilitado só com todos os itens marcados e o login gerado preenchido.
   - Assinatura em `aguardando_humano`: "Aguardando assinatura do cliente desde dd/mm hh:mm" e botão secundário "Reenviar lembrete".
3. Coluna lateral: dados do cliente (CNPJ, contato, plano, comercial) com "Copiar dados".
4. Log de auditoria, colapsado por padrão, em ordem cronológica.
5. "Cancelar onboarding" no rodapé (só backoffice).

### Ações e interações
- "Tentar novamente" → reexecuta só a etapa com erro, com a mesma chave de idempotência; zera o contador de tentativas automáticas.
- "Marcar como feito" → conclui a etapa manual registrando o usuário e o login informado; a esteira segue para a etapa 6.
- "Reenviar lembrete" → pede à D4Sign o reenvio do e-mail de assinatura. No máximo 1 por dia.
- "Cancelar onboarding" → modal com motivo obrigatório → status `cancelado`; se algum acesso já foi criado, o log lista quais precisam ser revogados à mão.
- Perfil comercial vê a linha do tempo e os dados do cliente; não vê botões nem o `erro_detalhe`.

---

## Tela: Histórico

**Objetivo:** responder "quanto demorou o cliente X" e auditar casos antigos.

### Hierarquia do conteúdo
1. Busca por nome da empresa ou CNPJ.
2. Tabela: empresa, status final (concluído ou cancelado), início, fim, tempo interno, tempo esperando assinatura, responsável.
3. Filtros por mês e por comercial.

### Ações e interações
- Clicar na linha → Detalhe do onboarding em modo leitura.
- "Exportar CSV" (só backoffice) com as colunas da tabela.

---

## Fluxo principal: iniciar onboarding (Fernanda)
1. No Painel, clica em "+ Novo onboarding".
2. Preenche empresa, CNPJ, contato, plano e comercial.
3. Clica em "Iniciar onboarding" e confirma no modal.
4. A etapa 1 envia o contrato pela D4Sign; o Detalhe mostra "Contrato enviado" com o id do envelope.

**Tempo esperado:** menos de 3 minutos do clique em "+ Novo" ao contrato enviado.

## Fluxo: assinatura e acessos automáticos (sem ninguém)
1. O cliente assina no e-mail da D4Sign.
2. O webhook marca a etapa 2 como concluída e grava `contrato_assinado_em`.
3. A etapa 3 cria o usuário no Sistema 1; a etapa 4 cria a conta no Sistema 2.
4. A etapa 5 vira `aguardando_humano` e a Fernanda recebe e-mail "Falta só o Sistema 3 para [empresa]".

**Tempo esperado:** menos de 2 minutos entre a assinatura e a tarefa manual aparecer.

Se o cliente não assinar em 5 dias úteis, a Fernanda recebe e-mail "Contrato de [empresa] parado há 5 dias" e decide entre "Reenviar lembrete" no Detalhe e cobrar por telefone. A etapa não vira erro.

## Fluxo: etapa manual do Sistema 3 (Fernanda)
1. Abre o Detalhe pelo e-mail ou pela faixa "Precisa de você".
2. Segue o checklist no Sistema 3 em outra aba, usando "Copiar dados".
3. Marca os itens, cola o login gerado e clica em "Marcar como feito".
4. A etapa 6 envia ao cliente o e-mail com os acessos e ao comercial o aviso de conclusão. Status vira `concluido`.

**Tempo esperado:** menos de 10 minutos.

## Fluxo: erro e destrave (Fernanda)
1. Uma etapa automática falha. Se a falha for técnica, o sistema tenta de novo sozinho em 1, 5 e 15 minutos.
2. Esgotadas as tentativas, ou se a falha for de dado, a etapa vira `erro`, o onboarding vira `com_erro` e a Fernanda recebe e-mail com a mensagem legível.
3. Ela abre o Detalhe, lê "O Sistema 2 recusou: e-mail já cadastrado", resolve a causa (no sistema interno ou corrigindo o e-mail do cliente) e clica em "Tentar novamente".
4. A etapa roda de novo e a esteira continua de onde parou.

## Fluxo: consulta do comercial (Bruno)
1. Abre o link do Embarque no celular; a sessão ainda está ativa.
2. O Painel abre com "Só os meus" ligado.
3. Toca no cliente e vê a etapa atual e há quanto tempo está nela.
4. Quando o onboarding conclui, recebe e-mail com o resumo e não precisa abrir a ferramenta.

**Tempo esperado:** menos de 30 segundos.

## Fluxo: cancelamento (Fernanda)
1. No Detalhe, clica em "Cancelar onboarding".
2. Escreve o motivo e confirma.
3. O onboarding sai do Painel e vai para o Histórico; o log lista acessos a revogar, se houver.

## Estados
- **Vazio (Painel sem onboarding ativo):** "Nenhum onboarding em andamento." e botão "+ Novo onboarding" para backoffice; para comercial, "Nenhum cliente seu em onboarding agora."
- **Vazio (Histórico):** "Nenhum onboarding concluído ainda."
- **Carregando:** esqueleto dos cards e da linha do tempo; nunca tela em branco.
- **Erro de etapa:** bloco da etapa com mensagem legível e "Tentar novamente"; o resto da linha do tempo continua visível.
- **Erro ao salvar o formulário:** os campos continuam preenchidos e a mensagem diz o que corrigir.
- **Sistema externo fora do ar (D4Sign, Sistema 1 ou 2):** faixa no topo do Painel "Sistema 2 sem resposta desde hh:mm. As etapas vão tentar de novo sozinhas." enquanto houver falha técnica em andamento.
- **Sem conexão:** faixa "Sem conexão. Os dados podem estar desatualizados." e botões de ação desabilitados até voltar. A esteira roda no servidor e não depende do navegador aberto.
- **Sem permissão:** perfil comercial que abre a URL de Novo onboarding vê "Só o backoffice inicia onboardings" e volta ao Painel.
