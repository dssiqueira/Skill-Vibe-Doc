# Decisões técnicas

*A mais recente em cima. Antes de reabrir uma decisão, traga um motivo que não estava aqui.*

## Mapa de autonomia por etapa

Resumo das decisões abaixo. Degraus, do mais baixo ao mais alto: sem IA, fluxo determinístico, fluxo com etapa de IA, agente de tarefa, agente autônomo. Nenhuma etapa passa do segundo degrau.

| Etapa | Degrau | Quem dispara | Onde entra o humano |
|---|---|---|---|
| Formulário de novo onboarding | Sem IA, manual | Fernanda | Preenche e confirma o resumo antes de qualquer envio ao cliente |
| 1. Envio do contrato | Fluxo determinístico | Confirmação do formulário | Já entrou: a confirmação é o portão. Erro de dado vai para ela |
| 2. Assinatura | Fluxo determinístico (espera evento externo) | Webhook da D4Sign | Só cobra o cliente se passar de 5 dias úteis |
| 3. Acesso Sistema 1 | Fluxo determinístico com 3 tentativas | Conclusão da etapa 2 | Só depois de esgotar as tentativas ou em erro de dado |
| 4. Acesso Sistema 2 | Fluxo determinístico com 3 tentativas | Conclusão da etapa 3 | Igual à etapa 3 |
| 5. Acesso Sistema 3 | Sem IA, manual guiado | Conclusão da etapa 4 | Executa a etapa inteira e marca como feito |
| 6. Notificações | Fluxo determinístico | Conclusão da etapa 5 | Não entra |
| Cancelamento | Sem IA, manual | Fernanda | Decide, escreve o motivo e revoga acessos à mão |

---

## 2026-03-18 Falha técnica tenta sozinha, falha de dado para na hora

- **Contexto:** as APIs dos Sistemas 1 e 2 caem algumas vezes por semana por poucos minutos, e a Fernanda não pode virar o botão de "tentar de novo" de cada instabilidade.
- **Decisão:** HTTP 5xx, timeout e 429 geram até 3 novas tentativas automáticas (1, 5 e 15 minutos). HTTP 4xx (e-mail já cadastrado, campo inválido) vai direto para `erro` e avisa a Fernanda. Toda chamada leva chave de idempotência, então repetir nunca duplica conta.
- **Alternativas descartadas:** tentar indefinidamente (esconde o problema e o cliente espera sem ninguém saber); nunca tentar sozinho (a Fernanda viraria operadora de retry, que é o trabalho que a ferramenta deveria tirar dela); tentar também em 4xx (repetir um dado errado só gera o mesmo erro três vezes).
- **Nível de autonomia:** fluxo determinístico. A regra "5xx tenta, 4xx para" cobre 100% dos casos que conhecemos; não há decisão ambígua que justifique IA classificando erro.
- **Onde entra o humano:** depois da terceira tentativa técnica falhar, ou na primeira falha de dado. Ela corrige a causa e clica em "Tentar novamente".

## 2026-03-12 Sistema 3 fica manual guiado, sem RPA

- **Contexto:** o Sistema 3 é legado, sem API, com tela que muda a cada atualização do fornecedor, e representa uma de seis etapas.
- **Decisão:** a etapa 5 é manual. A ferramenta gera o checklist com os dados prontos para copiar, avisa a Fernanda por e-mail e registra quem fez, quando e o login gerado. A esteira espera por ela.
- **Alternativas descartadas:** RPA (Playwright ou UiPath) clicando na tela do Sistema 3: quebra a cada mudança de layout, falha em silêncio e exigiria guardar credencial de usuário humano num robô. Agente de IA operando a tela (computer use): mesmo problema com custo e imprevisibilidade maiores, numa etapa que cria acesso, onde erro é incidente de segurança. Pular o Sistema 3 da ferramenta: perderíamos a visibilidade de que o cliente ainda não está ativo.
- **Nível de autonomia:** sem IA, execução humana. O degrau seguinte (fluxo determinístico) exige API, que não existe. São no máximo 50 execuções por mês, de cerca de 5 minutos cada: pouco mais de 4 horas mensais, que não pagam a manutenção de um robô.
- **Onde entra o humano:** a etapa inteira. Reavaliar se o Sistema 3 ganhar API ou se a etapa 5 virar a maior parte do tempo interno em `metricas.md`.

## 2026-03-10 Nenhuma etapa usa IA

- **Contexto:** a primeira versão do pedido sugeria "um agente que cuida do onboarding". O processo tem seis etapas fixas, entrada estruturada vinda de formulário e as mesmas regras para todo cliente.
- **Decisão:** a esteira é um fluxo determinístico. Nenhuma etapa chama modelo de linguagem.
- **Alternativas descartadas:** agente de tarefa que lê o e-mail do comercial e preenche o formulário (o formulário leva 2 minutos e o erro de extração mandaria contrato para o e-mail errado, ação irreversível); etapa de IA que escreve a mensagem de erro para a Fernanda (as mensagens possíveis são poucas e conhecidas, um mapa de código para frase resolve); agente autônomo que decide a ordem das etapas (a ordem é regra de negócio, não decisão).
- **Nível de autonomia:** fluxo determinístico. Não houve etapa em que o degrau mais baixo falhasse: entrada estruturada, regra fixa e ação com efeito externo pedem previsibilidade, e a auditoria exige explicar cada passo.
- **Onde entra o humano:** no formulário (confirmação antes do envio), na etapa manual do Sistema 3, em erros e no cancelamento. Ver o mapa no topo.

## 2026-03-05 Orquestração no próprio Postgres, com pg_cron e Edge Functions

- **Contexto:** a esteira precisa de estado durável, novas tentativas agendadas, espera de dias pela assinatura e log de auditoria de cada passo, para 10 a 50 onboardings por mês.
- **Decisão:** o estado de cada etapa mora em EtapaOnboarding no Supabase Postgres. `pg_cron` roda a cada minuto, acha etapas prontas e chama a Edge Function correspondente. Log de auditoria na mesma transação.
- **Alternativas descartadas:** n8n ou Make (o fluxo ficaria fora do repositório, sem revisão de código, e o log de auditoria se dividiria entre duas ferramentas); Temporal ou Inngest (resolvem durabilidade muito bem, mas são mais um serviço e mais um conceito para um volume de 2 execuções por dia útil); fila em Redis (mais infraestrutura, e o estado ainda precisaria ir para o banco para o painel ler).
- **Nível de autonomia:** não envolve IA.
- **Onde entra o humano:** não se aplica. Se o volume passar de 500 onboardings por mês ou surgirem fluxos paralelos, reavaliar Inngest.

## 2026-03-03 D4Sign para assinatura digital

- **Contexto:** precisamos enviar contrato por API e saber por webhook quando foi assinado, com validade jurídica no Brasil.
- **Decisão:** D4Sign, com um modelo de contrato por plano e webhook de documento finalizado.
- **Alternativas descartadas:** DocuSign (API mais completa, mas cobrança em dólar e plano com API acima do volume da empresa); Clicksign (equivalente técnico; a empresa já tinha conta D4Sign para outros contratos); manter e-mail com PDF (é o problema que estamos resolvendo).
- **Nível de autonomia:** não envolve IA.
- **Onde entra o humano:** o cliente assina. Se a D4Sign trocar de preço ou a empresa migrar, a etapa 1 e o `webhook-d4sign` são os únicos pontos a mudar.
