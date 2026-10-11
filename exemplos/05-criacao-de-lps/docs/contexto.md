# Contexto do produto

## Problema
Criar uma landing page bem escrita exige copywriter, designer e desenvolvedor. Para validar uma ideia, abrir lista de espera ou dar um endereço profissional a um serviço, esse custo (de R$ 1.500 a R$ 5.000 com freelancer, ou um fim de semana inteiro no Carrd) não se paga. O resultado é uma LP genérica, com a cara de qualquer template, ou nenhuma LP. E quando a pessoa já tem marca (cores, fonte, logo, às vezes até um DESIGN.md do próprio produto), a ferramenta ignora isso e entrega uma página que não parece dela.

## Solução
Ferramenta web que gera uma landing page completa a partir de um briefing curto e da identidade visual da marca. Exemplo real: Rodrigo termina o MVP do seu SaaS numa sexta à noite, abre a ferramenta, sobe o DESIGN.md que já usa no código do produto, responde cinco perguntas sobre o produto e o público, e em menos de 15 segundos tem uma LP de lista de espera com as cores, a fonte e os cantos da marca dele. Ajusta duas frases no painel e exporta um HTML único para publicar na Vercel.

Divisão de trabalho:
- **A IA escreve:** headline, subheadline, benefícios, como funciona, perguntas frequentes, texto do CTA e rodapé, e escolhe a ordem das seções conforme o tipo de produto.
- **O DESIGN.md da marca decide:** cores, tipografia, cantos, espaçamento e estilo dos componentes. A IA nunca escolhe cor nem fonte.
- **O código decide:** o HTML e o CSS, montados por templates determinísticos a partir do texto gerado e dos tokens da marca.
- **O usuário controla:** todo texto pode ser editado antes de exportar, e nada é publicado sem ele exportar.

## Audiência principal
Founder técnico que acabou de construir (ou está validando) um produto, sabe o que ele faz, não sabe escrever copy e quer uma LP com a cara da marca numa noite, sem contratar ninguém.

## Escopo do MVP
- Briefing guiado, uma pergunta por vez (produto, descrição, público, tom, objetivo do CTA).
- Marca da página: importar um DESIGN.md existente, gerar um a partir de cor, fonte e logo, ou usar um tema padrão.
- Geração dos textos pela IA e montagem da página com os tokens da marca, em menos de 15 segundos.
- Preview com edição de texto inline, refletindo em tempo real.
- Exportação em HTML único (CSS embutido, logo embutido) junto com o DESIGN.md usado.
- Histórico de páginas e de marcas salvas, com plano free (3 gerações por mês) e pro.

## O que NÃO é (pelo menos agora)
- Não é construtor visual: sem arrastar e soltar, sem editor de código, sem ajuste de cor dentro da tela de edição (cor muda na marca, não na página).
- Não hospeda páginas nem conecta domínio ou DNS. Entrega o arquivo para o usuário publicar onde quiser.
- Não é CMS: não tem edição contínua de página publicada nem blog.
- Não gera imagens nem fotos. Usa o logo da marca e blocos tipográficos.
- Não inventa prova social: depoimentos, números de clientes e logos de parceiros saem como espaço marcado para o usuário preencher.
- Não extrai identidade visual de um site por URL (fica para depois do MVP).

## Critério de sucesso
Em 90 dias após o lançamento: 40% das gerações chegam à exportação, 30% das páginas exportadas usam uma marca importada ou gerada (não o tema padrão), e 4% dos usuários free assinam o pro.

## Critério de morte
Se, 90 dias após o lançamento, menos de 20% das gerações forem exportadas, ou se mais de 60% das páginas exportadas tiverem metade ou mais dos textos reescritos pelo usuário, a premissa de que a IA entrega copy publicável está errada: parar e revisar o gerador antes de investir em aquisição. Se a conversão free para pro ficar abaixo de 1,5% no mesmo prazo, revisar o modelo de cobrança.
