# Decisões técnicas

*A mais recente em cima. Antes de reabrir uma decisão, traga um motivo que não estava aqui.*

---

## 2026-03-18 Guardrails da geração: o que a IA não pode escrever

- **Contexto:** a IA escreve texto que vai ao ar com o nome do usuário, e parte da base (como a Mariana) é de profissão regulada e não revisa o que publica.
- **Decisão:** cinco travas, todas no servidor:
  1. **Esquema fechado:** a resposta precisa passar no esquema Zod de `conteudo_gerado` (tipos de seção permitidos, limite de caracteres por campo, ex.: headline até 70). Falhou duas vezes, a geração falha sem consumir crédito.
  2. **Sem prova social inventada:** depoimentos, números de clientes, notas e logos de parceiros saem sempre como placeholder marcado. Um validador rejeita números e aspas fora dos campos permitidos.
  3. **Sem promessa de resultado em saúde e finanças:** o prompt de sistema proíbe e um filtro de termos ("garantido", "em X dias", "renda extra de R$") remove a frase e marca o bloco com "Revise antes de publicar", sem nova chamada à IA.
  4. **Briefing é dado, não instrução:** o texto do usuário vai delimitado e com a instrução de nunca obedecer comandos dentro dele; o HTML final é montado pelo template, então nenhum texto gerado vira script, link ou estilo. Todo texto é escapado.
  5. **Recusa de oferta proibida:** briefing de pirâmide financeira, medicamento sem receita ou conteúdo adulto é recusado por uma lista de categorias no servidor antes da chamada ou pelo próprio modelo, que pode devolver `recusa` no esquema; nos dois casos aparece a mensagem de recusa e o crédito não é consumido.
- **Alternativas descartadas:** confiar só no prompt de sistema (falha em casos de borda e não deixa rastro); revisão humana antes de exportar (mata o "pronto em 2 minutos").
- **Nível de autonomia:** fluxo com etapa de IA, com validação determinística depois.
- **Onde entra o humano:** o usuário revê no preview e é avisado dos placeholders antes de exportar; nada é publicado pelo produto.

## 2026-03-12 Custo de IA: uma chamada por geração, com teto

- **Contexto:** o plano free é a aquisição e cada geração custa dinheiro; regerar sem limite pode tornar o pro deficitário.
- **Decisão:** uma única chamada ao modelo de linguagem por geração, com prompt de sistema e contexto da marca em cache de prompt, saída limitada a 2.500 tokens. Meta de custo: até R$ 0,15 por geração e até R$ 0,40 por página exportada. Free com 3 gerações por mês e 1 por sessão anônima; pro com uso justo de 100 por mês. Editar texto e reaplicar marca nunca chamam a IA. O modelo é escolhido por configuração (`LLM_MODEL`): o de custo intermediário do provedor, porque o mais barato errou o esquema JSON e o tom em teste com 50 briefings reais, e o mais caro não melhorou a taxa de edição o suficiente para pagar a diferença.
- **Alternativas descartadas:** uma chamada por seção (mais controle, 6 vezes mais latência e custo); gerar várias variações e deixar o usuário escolher (triplica o custo e contradiz o "pronto de primeira"); regerar seção individual no MVP (fica para depois, se a métrica de edição mostrar uma seção recorrente).
- **Nível de autonomia:** fluxo com etapa de IA. Um fluxo determinístico (templates com lacunas) não escreve copy específica do produto, que é o valor central.
- **Onde entra o humano:** o time revisa o custo por página exportada toda semana; o alerta de R$ 150 por dia dispara revisão do teto.

## 2026-03-05 A IA escreve texto, o template monta o HTML

- **Contexto:** a versão inicial pedia à IA o HTML e o CSS completos; o resultado variava a cada geração, ignorava a marca e às vezes quebrava no celular.
- **Decisão:** a IA devolve só JSON (ordem das seções e textos). O HTML sai de templates React renderizados no servidor, um por tipo de seção, todos responsivos e semânticos, que recebem os tokens da Marca como variáveis CSS.
- **Alternativas descartadas:** IA gerando HTML livre (inconsistente, inseguro, caro em tokens); IA gerando HTML com lista de classes Tailwind permitidas (ainda quebra layout e não garante contraste).
- **Nível de autonomia:** fluxo com etapa de IA restrita ao texto. O visual é determinístico porque precisa ser previsível e fiel à marca.
- **Onde entra o humano:** não se aplica.

## 2026-03-02 A marca entra como DESIGN.md, importado ou gerado

- **Contexto:** a página precisa ter a cara da marca do usuário, e parte do público (como o Rodrigo) já mantém um DESIGN.md no repositório do produto.
- **Decisão:** a Marca é guardada como DESIGN.md no padrão aberto do Google. Quem tem, importa; quem não tem, monta em 4 campos e o produto escreve o arquivo com código determinístico; quem não quer, usa um tema pronto (que também é um DESIGN.md). Todo arquivo passa pelo lint oficial antes de ser usado, com correção automática de contraste quando possível. O DESIGN.md é exportado junto com a página.
- **Alternativas descartadas:** formato próprio de tema (prende o usuário e não conversa com os agentes de código dele); IA gerando a paleta a partir de uma descrição (resultado imprevisível e contraste não garantido); extrair a marca de um site por URL (útil, mas frágil; fica para depois do MVP).
- **Nível de autonomia:** sem IA. Montar e validar tokens é regra fixa; IA aqui só adicionaria variação indesejada.
- **Onde entra o humano:** o usuário vê a miniatura e aprova; correções automáticas de contraste são sempre avisadas.

## 2026-02-26 Supabase como banco, auth e storage

- **Contexto:** um dev sozinho precisa de auth, Postgres, storage de logo e regras de acesso sem manter servidor.
- **Decisão:** Supabase (Auth, Postgres com RLS, Storage, pg_cron), com app Next.js na Vercel.
- **Alternativas descartadas:** Firebase (modelo de documentos atrapalha consultas de histórico e de custo por usuário); Postgres próprio com NextAuth (mais peças para manter sem ganho no MVP).
- **Nível de autonomia:** não se aplica.
- **Onde entra o humano:** não se aplica.
