# Decisões técnicas

*A mais recente em cima. Antes de reabrir uma decisão, traga um motivo que não estava aqui.*

---

## 2026-03-18 Sem IA no match nem no preço

- **Contexto:** surgiu a ideia de usar um modelo de linguagem para classificar a descrição do pedido na categoria certa, sugerir faixa de preço ao morador e ranquear as propostas.
- **Decisão:** nenhuma etapa de IA no MVP. Categoria é escolhida pela pessoa entre 5 opções; quem vê o pedido é decidido por regra (categoria, raio, disponibilidade); propostas aparecem por ordem de chegada.
- **Alternativas descartadas:** classificação por IA (com 5 categorias visuais a pessoa acerta sozinha em um toque, e erro de classificação esconde o pedido de quem atenderia); sugestão de preço (cria expectativa que o profissional não cumpre e vira briga na avaliação); ranking de propostas (o morador perde a confiança se não entende por que uma proposta aparece em cima).
- **Nível de autonomia:** sem IA. O fluxo determinístico resolve a dor inteira; o gargalo do marketplace é liquidez, não inteligência. Reavaliar classificação quando houver mais de 15 categorias.
- **Onde entra o humano:** o morador escolhe a categoria e a proposta; o profissional decide se responde.

---

## 2026-03-12 Contato pelo WhatsApp depois do aceite, sem chat interno

- **Contexto:** depois do aceite, morador e profissional precisam combinar horário, detalhe e pagamento.
- **Decisão:** o app libera telefone e endereço só depois do aceite e abre o WhatsApp com mensagem pronta (`wa.me`). Nada de chat dentro do app.
- **Alternativas descartadas:** chat interno com Supabase Realtime (semanas de trabalho, notificação, moderação, e as duas personas já vivem no WhatsApp); mostrar telefone antes do aceite (profissional recebe ligação de quem só está cotando preço e o morador é assediado por todos que mandaram proposta).
- **Onde entra o humano:** a negociação inteira acontece entre os dois, fora do app.

---

## 2026-03-10 Login por telefone com código SMS, sem senha

- **Contexto:** o Seu João esquece senha e desiste; o produto depende de um telefone confiável para o contato depois do aceite.
- **Decisão:** Supabase Auth com OTP por SMS (Twilio Verify). Email coletado no cadastro só para notificação.
- **Alternativas descartadas:** email e senha (recuperação de senha é onde o profissional desiste, e o telefone continuaria sem verificação); login com Google (rápido para a Cláudia, mas não entrega telefone verificado e parte dos profissionais não lembra a conta Google do celular); link mágico por email (o profissional confere email poucas vezes por dia).
- **Custo aceito:** cerca de R$ 0,30 por SMS enviado. Com teto de 5 tentativas e reenvio a cada 60 segundos, o gasto no piloto fica abaixo de R$ 300 por mês. <!-- sugestão: confirmar preço do Twilio -->

---

## 2026-03-05 PostGIS no Supabase para raio de atendimento

- **Contexto:** profissional vê pedidos dentro do raio dele, e o Início público conta profissionais que atendem um CEP.
- **Decisão:** guardar `localizacao` como `geography` e calcular distância em linha reta no banco com `ST_DWithin`. Geocodificação pelo Google uma única vez por endereço salvo.
- **Alternativas descartadas:** Google Distance Matrix para distância por rua (custo por par profissional e pedido cresce rápido e a precisão extra não muda a decisão de quem atende num raio de 10 km); filtrar só por cidade ou bairro (Campinas tem bairros grandes e o profissional atende bairros vizinhos de outras cidades); Firebase com geohash (exigiria segunda base e regras de acesso duplicadas).

---

## 2026-03-02 Next.js, Supabase e Vercel como stack

- **Contexto:** equipe de uma pessoa, precisa de auth, banco relacional com regra de acesso, storage e cron sem montar servidor.
- **Decisão:** Next.js (App Router) com TypeScript na Vercel, Supabase para auth, Postgres, storage e cron, Tailwind com tema gerado do DESIGN.md. Web responsiva instalável como PWA, sem app nativo.
- **Alternativas descartadas:** app nativo com React Native (loja, revisão e atualização atrasam o piloto, e a Cláudia não instala app para um serviço pontual); Firebase (modelo de documentos complica as relações entre pedido, proposta e avaliação e a RLS fica espalhada em regras); backend próprio em Node (mais coisa para manter sem ganho para o MVP).
