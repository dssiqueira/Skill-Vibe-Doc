# Contexto do produto

*Marketplace de dois lados. A IA tende a construir só o lado de quem pede; aqui os dois lados são produto, e o MVP só existe se os dois funcionarem.*

## Problema

- **Morador (demanda):** quando a torneira pinga ou a casa precisa de faxina antes de uma visita, a solução hoje é pedir indicação em grupo de WhatsApp do prédio. Leva de horas a dias, não há avaliação nem histórico, e a pessoa coloca um desconhecido dentro de casa sem referência nenhuma.
- **Profissional (oferta):** eletricista, encanador, diarista e pintor autônomos dependem de indicação boca a boca. Em mês fraco ficam com dias vazios na agenda e não têm como mostrar o próprio trabalho para quem não os conhece.

## Solução

A Cláudia abre o Resolve Aí no celular, digita o CEP e escolhe "Hidráulica". Vê que 7 profissionais atendem o bairro dela, descreve "Torneira da cozinha pingando" em uma frase, marca como urgente e publica. Em menos de 2 horas recebe 3 propostas com valor, prazo, nota e avaliações de outros moradores. Aceita a do Seu João (4,8 com 23 avaliações), o app libera o telefone dele e os dois combinam pelo WhatsApp. Depois do serviço, ela marca como concluído e avalia.

Do outro lado, o Seu João deixa o app em "Disponível", recebe um email de pedido novo na região dele, vê bairro, distância e descrição, e manda proposta em menos de 1 minuto.

## Audiência principal

Dois lados, uma persona principal por lado (detalhes em `personas.md`):
- **Demanda:** morador de cidade grande, 30 a 55 anos, que trabalha fora e precisa resolver serviço doméstico pontual pelo celular, com pressa.
- **Oferta:** profissional autônomo de serviço doméstico, 35 a 60 anos, com clientela por indicação, pouca paciência para app e muito WhatsApp.

Lançamento em uma cidade piloto, Campinas (SP), com 5 categorias. <!-- sugestão: confirmar cidade -->

## Escopo do MVP

1. Consulta de cobertura sem login: CEP e categoria mostram quantos profissionais atendem a região.
2. Cadastro por telefone com código SMS, escolhendo o lado (morador ou profissional).
3. Morador publica pedido (categoria, título, descrição, urgência, data preferida, endereço).
4. Profissional cadastra perfil (categorias, raio, foto, bio, até 6 fotos de trabalho), liga a disponibilidade e vê pedidos dentro do raio e das categorias dele.
5. Profissional envia proposta (valor, prazo, mensagem); morador compara e aceita uma; o app libera o contato dos dois.
6. Conclusão do pedido e avaliação do profissional pelo morador (nota de 1 a 5 e comentário).

## O que NÃO é (pelo menos agora)

- Não é plataforma de emprego nem agência: o profissional é autônomo e o Resolve Aí não garante o serviço.
- Não tem pagamento dentro do app. Valor e forma de pagamento são combinados entre os dois, fora da plataforma.
- Não tem chat interno. Depois do aceite, a conversa vai para o WhatsApp ou telefone.
- Não atende empresa nem condomínio como cliente (sem B2B, sem nota fiscal, sem contrato recorrente).
- Não tem agendamento com calendário nem serviço recorrente automático.
- Não tem app nativo. É web responsiva, instalável como PWA.

## Critério de sucesso

Em 90 dias após o lançamento em Campinas:
- 60% dos pedidos publicados recebem pelo menos 1 proposta em até 24 horas;
- 30% dos pedidos publicados chegam a "em andamento" (proposta aceita);
- 50 profissionais ativos por semana (enviaram pelo menos 1 proposta nos últimos 7 dias).

## Critério de morte

Se no dia 90 menos de 30% dos pedidos receberem proposta em 24 horas, ou houver menos de 20 profissionais ativos por semana, o marketplace aberto para. A revisão considera duas saídas: reduzir para uma categoria só (a de maior demanda em `pedido_aberto`) com profissionais recrutados à mão, ou encerrar.
