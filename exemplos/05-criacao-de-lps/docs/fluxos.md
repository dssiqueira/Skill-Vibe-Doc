# Fluxos e telas

*Aqui fica o que existe no produto e por onde a pessoa anda. Cor, fonte e estilo ficam no DESIGN.md.*

## Princípios de experiência
1. **Resultado antes de compromisso.** A pessoa vê a própria página gerada antes de criar conta. Cadastro só para salvar ou exportar.
2. **Uma pergunta por vez.** O briefing nunca mostra mais de um campo por passo. Do primeiro campo à página pronta: até 2 minutos.
3. **O preview é a estrela.** A interface do produto é neutra e recua; a página gerada, com a cara da marca, ocupa o maior espaço da tela.
4. **A marca manda no visual, a IA manda no texto.** Nenhuma tela oferece ajuste de cor ou fonte da página; quem quer mudar visual edita a Marca.
5. **Celular resolve tudo.** Todo fluxo funciona com uma mão no celular (pensando na Mariana); no notebook, a mesma coisa com mais espaço.

## Mapa de telas
- **Home pública:** explicar em 5 segundos o que a ferramenta faz e levar ao briefing.
- **Briefing:** coletar produto, descrição, público, tom, objetivo do CTA e marca, uma pergunta por vez.
- **Marca (passo do briefing):** escolher entre importar DESIGN.md, montar a marca em 4 campos ou usar tema padrão.
- **Gerando:** segurar a atenção por até 15 segundos enquanto a página é gerada.
- **Preview e edição:** ver a página com a marca aplicada e editar os textos.
- **Exportar (modal):** baixar o HTML e o DESIGN.md, com instrução de publicação.
- **Criar conta (modal):** cadastro com Google ou e-mail, sem perder o que foi gerado.
- **Minhas páginas:** histórico de páginas geradas, com exportar e arquivar.
- **Minhas marcas:** lista de marcas salvas, com editar, baixar DESIGN.md e definir padrão.
- **Planos:** comparar free e pro e assinar.

---

## Tela: Home pública

**Objetivo:** convencer em 5 segundos e começar o briefing sem cadastro.

### Hierarquia do conteúdo
1. Promessa em uma linha ("Sua landing page, com a cara da sua marca, em 2 minutos") e botão "Criar minha página".
2. Três exemplos de páginas geradas com marcas diferentes, lado a lado (empilhados no celular).
3. Como funciona em 3 passos: conte sobre o produto, traga sua marca, exporte o HTML.
4. Planos resumidos e link para entrar.

### Ações e interações
- "Criar minha página" → abre o Briefing no passo 1 e dispara `briefing_iniciado`.
- "Entrar" → modal Criar conta, aba de login.

---

## Tela: Briefing

**Objetivo:** coletar o mínimo para gerar uma página boa, sem parecer formulário.

### Hierarquia do conteúdo
1. A pergunta atual, grande, com o campo logo abaixo.
2. Exemplo de resposta como placeholder (ex.: "App que organiza a fila de espera de barbearias pelo WhatsApp, para donos de barbearia com 2 a 5 cadeiras").
3. Barra de passos (6 passos) e botão "Voltar".

### Passos em sequência
1. "Como se chama seu produto ou serviço?" (texto curto, até 60 caracteres)
2. "O que ele faz e para quem?" (texto longo, 40 a 1.200 caracteres, contador visível)
3. "Quem você quer que leia essa página?" (texto curto, até 300 caracteres)
4. "Qual o tom da página?" (4 cartões de opção: Profissional, Descontraído, Urgente, Inspirador, cada um com uma frase de exemplo)
5. "O que o botão principal deve fazer?" (4 cartões: Lista de espera, Fale comigo, Comprar, Cadastrar) e o campo do destino do botão (URL, e-mail ou WhatsApp, conforme a opção)
6. "Qual a cara da página?" (passo Marca, abaixo) e botão "Gerar minha página"

### Ações e interações
- Enter ou "Continuar" avança; o campo seguinte aparece com foco.
- Campo inválido não avança e mostra o motivo abaixo do campo ("Conte um pouco mais: mínimo de 40 caracteres").
- O rascunho do briefing fica salvo no navegador; recarregar a página não perde respostas.

---

## Tela: Marca (passo 6 do briefing)

**Objetivo:** definir a identidade visual que o gerador vai aplicar, em menos de 1 minuto.

### Hierarquia do conteúdo
1. Se o usuário tem marcas salvas: lista das marcas com miniatura (cor primária, fonte, canto), a padrão pré-selecionada.
2. Três cartões de opção:
   - **Tenho um DESIGN.md:** subir o arquivo ou colar o conteúdo.
   - **Montar minha marca:** cor principal, cor de apoio, fonte (lista de 12 fontes do Google Fonts) e estilo de canto (reto, suave, arredondado), mais logo opcional (PNG ou SVG, até 1 MB).
   - **Usar um tema pronto:** Minimalista, Bold, Corporativo ou Colorido, com miniatura.
3. Miniatura ao vivo de um bloco de página (título, parágrafo, botão) com a marca aplicada.

### Ações e interações
- Subir ou colar DESIGN.md → o produto valida (lint) na hora. 0 erros: mostra a miniatura e dispara `marca_importada`. Com erro: lista os erros em linguagem simples ("O texto do botão sobre a cor primária tem contraste 3,1:1; o mínimo é 4,5:1") e oferece "Corrigir automaticamente" (ajusta a cor `on-` para preto ou branco, o que tiver mais contraste) e dispara `marca_lint_falhou`.
- Montar minha marca → o produto escreve o DESIGN.md a partir dos 4 campos, valida o contraste e escurece a cor principal até 4,5:1 se precisar, avisando. Dispara `marca_gerada`.
- Tema pronto → usa a Marca padrão do tema, sem evento extra.
- Sem conta, a Marca vive só na sessão; ao criar conta, é salva em Minhas marcas.

---

## Tela: Gerando

**Objetivo:** segurar a atenção por até 15 segundos sem prometer o que não sabe.

### Hierarquia do conteúdo
1. Esqueleto da página já com as cores e a fonte da Marca (o visual aparece antes do texto).
2. Mensagens que se revezam: "Escrevendo a headline...", "Montando os benefícios...", "Aplicando sua marca...".

### Ações e interações
- Sem percentual de progresso.
- Ao concluir, vai direto para Preview e edição e dispara `geracao_concluida`.
- Passou de 25 segundos ou a resposta da IA veio inválida duas vezes: estado de erro (abaixo) e `geracao_falhou`.

---

## Tela: Preview e edição

**Objetivo:** ver a página com a marca aplicada, ajustar o texto e exportar.

### Hierarquia do conteúdo
1. Preview da página em iframe (60% da largura no notebook), com alternância Desktop/Celular.
2. Botão "Exportar" fixo no topo direito.
3. Painel de edição à esquerda: uma seção por bloco da página, na mesma ordem, com os textos em campos editáveis.
4. Blocos de prova social marcados como "Preencha antes de publicar" e blocos em que o filtro de conteúdo removeu uma frase marcados como "Revise antes de publicar".
5. "Gerar novamente" (secundário) com o aviso "usa 1 crédito" e o contador de créditos do mês.

No celular: abas "Ver página" e "Editar texto" no lugar das duas colunas; "Exportar" fixo no rodapé.

### Ações e interações
- Editar campo → preview atualiza em até 200 ms; ao sair do campo, grava em `textos_editados` e dispara `texto_editado`.
- Tocar num texto do preview → rola o painel até o campo correspondente e coloca foco nele.
- "Desfazer edições" num bloco → volta ao texto gerado daquele bloco.
- "Gerar novamente" → confirma o consumo de crédito, volta para Gerando com o mesmo briefing e a mesma Marca e dispara `pagina_regerada`.
- "Exportar" sem conta → modal Criar conta; com conta → modal Exportar.

### O que não aparece
- Editor de código ou HTML.
- Controle de cor, fonte ou espaçamento (o caminho é editar a Marca).

---

## Tela: Exportar (modal)

**Objetivo:** entregar arquivos prontos para publicar e ensinar a publicar.

### Hierarquia do conteúdo
1. Aviso, se houver bloco de prova social com placeholder: "2 blocos ainda estão com texto de exemplo" com "Voltar e preencher" e "Exportar sem esses blocos".
2. Botão "Baixar página (.html)": um arquivo só, com CSS e logo embutidos.
3. Botão "Baixar DESIGN.md da marca", para reaproveitar em outros projetos e agentes.
4. Guia curto de publicação em três abas: Vercel, Netlify, "Não sei o que é isso" (passo a passo com prints, pensado para a Mariana).

### Ações e interações
- Baixar página → gera o HTML com `textos_editados` aplicados, grava `html_exportado`, muda o status para `exportada` e dispara `pagina_exportada`.

---

## Tela: Criar conta (modal)

**Objetivo:** converter quem já viu o resultado, sem perder nada.

### Hierarquia do conteúdo
1. "Crie sua conta para salvar e exportar esta página."
2. Botão "Continuar com Google".
3. E-mail e senha.

### Ações e interações
- Conta criada → briefing, Marca e página da sessão migram para o usuário, dispara `conta_criada` e o modal Exportar abre em seguida.

---

## Tela: Minhas páginas

**Objetivo:** reencontrar e reexportar páginas.

### Hierarquia do conteúdo
1. Botão "Nova página".
2. Lista com miniatura, nome, marca usada, data e status (Pronta, Exportada).
3. Filtro "Arquivadas".

### Ações e interações
- Tocar no item → Preview e edição.
- "Exportar" no item → modal Exportar.
- "Arquivar" → confirma e move para Arquivadas (não apaga).
- Página gerada com uma versão antiga da Marca mostra "Marca atualizada: reaplicar?" → remonta o HTML com a versão nova, sem chamar a IA e sem consumir crédito.

---

## Tela: Minhas marcas

**Objetivo:** manter a identidade visual que as páginas usam.

### Hierarquia do conteúdo
1. Lista de marcas com miniatura, origem (Importada, Montada, Tema) e quantas páginas usam.
2. Ações por marca: editar, baixar DESIGN.md, definir como padrão.

### Ações e interações
- Editar abre o mesmo formulário de "Montar minha marca" ou a área de colar DESIGN.md, conforme a origem; salvar valida o lint e cria nova versão.

---

## Tela: Planos

**Objetivo:** mostrar o que o pro libera e assinar sem atrito.

### Hierarquia do conteúdo
1. Free: 3 gerações por mês. Pro: gerações ilimitadas (uso justo de 100 por mês) e marcas ilimitadas.
2. Botão "Assinar pro" → Stripe Checkout; dispara `assinatura_iniciada`.
3. Para quem já é pro: "Gerenciar assinatura" (Stripe Customer Portal).

---

## Fluxo principal: Rodrigo cria a LP de lista de espera com o DESIGN.md do produto
1. Home pública → "Criar minha página".
2. Responde os passos 1 a 5 (nome, descrição, público, tom Descontraído, CTA Lista de espera com link do formulário).
3. No passo Marca, escolhe "Tenho um DESIGN.md" e cola o arquivo do repositório. Lint passa; miniatura aparece.
4. "Gerar minha página" → Gerando → Preview.
5. Edita a headline e um benefício.
6. "Exportar" → cria conta com Google → baixa o HTML.

**Tempo esperado:** até 5 minutos do primeiro clique ao HTML baixado; geração em menos de 15 segundos.

## Fluxo: Mariana monta a marca pelo celular
1. Chega pelo link na bio de um perfil parceiro, no celular.
2. Responde os passos 1 a 5 (tom Profissional, CTA Fale comigo com o número de WhatsApp).
3. No passo Marca, escolhe "Montar minha marca": cor principal (verde do Instagram), cor de apoio, fonte, canto arredondado e logo.
4. O produto avisa que escureceu o verde para o texto ficar legível e mostra a miniatura.
5. Gera, olha a página na aba "Ver página", não edita nada.
6. Exporta, cria conta com e-mail e segue a aba "Não sei o que é isso" do guia de publicação.

**Tempo esperado:** até 8 minutos, sem tocar em nenhum termo técnico.

## Fluxo: gerar novamente
1. No Preview, "Gerar novamente" → confirma o uso de 1 crédito.
2. Nova página gerada com o mesmo briefing e a mesma Marca; a anterior fica em Minhas páginas.

## Fluxo: limite do plano free
1. Usuário free com 3 gerações no mês toca em "Gerar minha página" ou "Gerar novamente".
2. Em vez de gerar, abre Planos com a mensagem "Você usou as 3 gerações de outubro" e dispara `limite_atingido`.
3. Briefing e Marca ficam salvos; ao assinar, a geração começa sozinha.

## Estados
- **Vazio (Minhas páginas):** "Nenhuma página ainda" com botão "Criar minha primeira página".
- **Vazio (Minhas marcas):** só a Marca do tema padrão, com "Importe seu DESIGN.md ou monte sua marca em 1 minuto".
- **Carregando:** esqueletos com o formato do conteúdo; na geração, a tela Gerando.
- **Erro na geração:** "Não conseguimos gerar sua página agora. Seu crédito não foi usado." com "Tentar de novo"; o briefing continua preenchido.
- **Erro de marca:** lista dos problemas do DESIGN.md em linguagem simples, com "Corrigir automaticamente" quando possível e "Usar tema pronto" como saída.
- **Briefing recusado:** quando o pedido cai nas regras de conteúdo (ver `docs/decisoes.md`), "Não geramos páginas para esse tipo de oferta" com o motivo em uma frase; não consome crédito.
- **Sem conexão:** banner "Sem conexão. Suas edições ficam salvas aqui e sobem quando a internet voltar."; "Gerar" e "Exportar" ficam desabilitados.
- **Sem permissão:** abrir página ou marca de outro usuário mostra "Esta página não existe ou não é sua" e volta para Minhas páginas.
