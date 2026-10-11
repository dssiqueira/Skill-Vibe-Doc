---
name: vibe-doc
description: Cria, atualiza e revisa o Vibe Doc de um projeto, o briefing que a IA lê antes de construir. Gera AGENTS.md, DESIGN.md (padrão aberto do Google) e a pasta docs com contexto, personas, dados, fluxos, métricas, integrações e decisões. Use quando a pessoa quer começar um produto com IA, documentar um projeto para agentes de código, criar ou ajustar um DESIGN.md, ou quando uma mudança no código deixou os docs para trás.
license: MIT
metadata:
  author: Douglas Siqueira (doug.ia.br)
  version: 3.0.0
---

# Vibe Doc

O Vibe Doc é o briefing que transforma prompt em produto. Um PRD é para um dev que faz perguntas. Um Vibe Doc é para uma IA que assume. Seu trabalho é fazer a IA assumir certo.

A estrutura que você gera e mantém:

```
AGENTS.md              porta de entrada: o que é o projeto e onde está cada coisa
DESIGN.md              a cara do produto: tokens de cor, tipo, espaço e componentes (padrão aberto do Google)
docs/
├── contexto.md        problema, audiência, escopo, o que não é, critério de sucesso e de morte
├── personas.md        quem usa, em que situação, o que evita
├── estruturadedados.md  entidades, campos, relações e regras de negócio
├── fluxos.md          telas, fluxos, hierarquia e estados vazios e de erro
├── metricas.md        o que medir, por quê, eventos a registrar
├── integracoes.md     autenticação, banco, APIs, infraestrutura
└── decisoes.md        decisões técnicas com data, alternativa descartada e motivo
```

Escreva os arquivos no idioma da pessoa. Os nomes dos arquivos ficam como estão.

## Escolha o modo

Leia o pedido e o projeto antes de decidir:

- **Criar**: não existe `docs/` nem `DESIGN.md`, ou a pessoa quer começar um produto. Vá para "Modo criar".
- **Atualizar**: os docs existem e algo mudou no código ou no plano (nova entidade, nova tela, nova integração, troca de tecnologia). Vá para "Modo atualizar".
- **Revisar**: a pessoa quer saber se os docs estão bons, ou vai começar uma sessão grande e quer conferir. Vá para "Modo revisar".
- **Migrar**: existe um Vibe Doc antigo com `layout.md`. Siga "Migrar da versão antiga" e depois revise.

Se o projeto tiver só parte da estrutura, complete o que falta no modo criar e trate o resto como atualização.

## Modo criar

1. **Entreviste antes de escrever.** Siga `references/entrevista.md`. Pergunte em blocos curtos (no máximo 3 perguntas por vez), na ordem: produto, pessoas, dados, fluxos, cara, conexões, medição. Se a pessoa já mandou material (PRD, print, link, conversa), extraia dali e pergunte só o que falta.
2. **Não invente o que define o produto.** Problema, público, escopo e o que o produto não é vêm da pessoa. Detalhes de execução (nome de evento, campo técnico, estado de erro) você pode propor, marcando com `<!-- sugestão: confirmar -->`.
3. **Gere os arquivos a partir de `templates/`.** Preencha tudo. Arquivo com seção vazia é pior que arquivo curto. Siga as regras de escrita de `references/arquivos.md`.
4. **Monte o DESIGN.md seguindo `references/design-md.md`.** Se a pessoa não tem identidade visual, proponha uma a partir das personas e do contexto e diga isso a ela em uma frase. Se ela mandou referências (site, print, marca), extraia cores, tipografia e forma dali.
5. **Rode a conferência** (seção "Conferência") e corrija o que falhar.
6. **Feche com o primeiro prompt.** Entregue à pessoa o prompt de abertura:
   > Leia o AGENTS.md e tudo o que ele aponta. Me confirme o que vamos construir, quem vai usar, qual a cara do produto e qual a primeira funcionalidade. Não escreva código ainda.

## Modo atualizar

1. Descubra o que mudou: leia o diff (`git diff`, `git log` recente) ou pergunte.
2. Mapeie a mudança para os arquivos afetados com a tabela de `references/manutencao.md`. Mexa só neles.
3. Edite no lugar. Não reescreva o arquivo inteiro para mudar uma linha.
4. Se a mudança for uma decisão técnica (trocou banco, escolheu biblioteca, decidiu não usar IA num fluxo), registre no `decisoes.md` com data, alternativa descartada e motivo.
5. Se mudou cor, fonte, espaçamento ou componente, atualize o DESIGN.md e rode `npx @google/design.md diff` contra a versão anterior quando possível.
6. Diga à pessoa, em uma linha por arquivo, o que você atualizou.

Quando você mesmo acabou de fazer uma mudança relevante no código durante a sessão, rode este modo antes de encerrar, sem esperar pedido. Docs que a IA atualiza não envelhecem.

## Modo revisar

Leia todos os arquivos e devolva uma lista curta, do mais grave para o menos grave, usando os critérios de `references/manutencao.md`:

- contradição entre arquivos (persona fala de celular, fluxo descreve tela de desktop);
- divergência entre docs e código (entidade no banco que não está em `estruturadedados.md`, tela que não está em `fluxos.md`, cor no CSS que não está no DESIGN.md);
- trecho vago que obriga a IA a chutar ("interface moderna", "usuários em geral", "métricas de engajamento");
- seção vazia ou genérica;
- falta do critério de sucesso ou de morte no `contexto.md`.

Para cada item: arquivo, o problema em uma frase, e a correção proposta. Corrija direto se a pessoa pedir.

## Migrar da versão antiga

O Vibe Doc antigo tinha seis arquivos, com `layout.md` misturando duas coisas.

1. Do `layout.md`, mova telas, fluxos, hierarquia, interações e estados para `docs/fluxos.md`.
2. Mova princípios visuais, cores, fontes, espaçamentos e estilo de componente para o `DESIGN.md` na raiz.
3. Apague o `layout.md` depois de conferir que nada ficou para trás.
4. Crie `AGENTS.md` e `docs/decisoes.md` se não existirem.
5. Acrescente ao `contexto.md` o critério de sucesso e o critério de morte, perguntando à pessoa.
6. Se houver arquivos de regra por ferramenta (`.cursorrules`, `.windsurfrules`, `CLAUDE.md` e afins) repetindo o mesmo conteúdo, reduza cada um a uma linha que aponta para o `AGENTS.md`. Para o Claude Code, um `CLAUDE.md` com `@AGENTS.md` basta.

## Conferência

Antes de entregar qualquer modo:

- [ ] Todo arquivo da estrutura existe e nenhum tem seção vazia ou com texto de exemplo esquecido.
- [ ] `contexto.md` diz o que o produto NÃO é e tem critério de sucesso e critério de morte com número e prazo.
- [ ] Toda entidade citada em `fluxos.md` existe em `estruturadedados.md`, e vice-versa.
- [ ] Toda persona aparece em pelo menos um fluxo.
- [ ] Todo evento de `metricas.md` nasce de uma ação descrita em `fluxos.md`.
- [ ] O DESIGN.md tem frontmatter válido e as seções na ordem do padrão. Se houver Node no ambiente, rode `npx @google/design.md lint DESIGN.md` e corrija os erros.
- [ ] O `AGENTS.md` aponta para todos os arquivos e cabe em uma tela.

## Arquivos de apoio

- `references/arquivos.md`: o que vai em cada arquivo e as regras de escrita.
- `references/entrevista.md`: o roteiro de perguntas do modo criar.
- `references/design-md.md`: o formato do DESIGN.md, com exemplo.
- `references/manutencao.md`: mapa de mudança para arquivo e critérios de revisão.
- `templates/`: os esqueletos de todos os arquivos.
- `exemplo/`: um Vibe Doc completo (app para personal trainers) para consultar o nível de detalhe esperado.
