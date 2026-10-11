# Contexto do produto

## Problema

Empresa B2B que fecha de 10 a 50 clientes por mês faz o onboarding inteiro à mão, com cinco passagens de bastão:

1. O comercial fecha a venda e preenche uma planilha com os dados do cliente.
2. O backoffice copia os dados da planilha e manda o contrato por e-mail.
3. Ninguém sabe se o cliente assinou sem abrir a caixa de entrada.
4. Depois da assinatura, o backoffice cria o acesso à mão em três sistemas internos (dois com API, um legado sem API).
5. O backoffice avisa o comercial por WhatsApp que o cliente está ativo.

Custo hoje: 3 a 5 dias úteis entre a venda e o primeiro acesso do cliente, cerca de 40 minutos de trabalho manual de backoffice por cliente, erro de digitação em CNPJ e e-mail que só aparece quando o acesso não funciona, e o comercial sem resposta quando o cliente reclama do prazo.

## Solução

O comercial fecha a venda às 10h. A Fernanda, do backoffice, preenche o formulário em 2 minutos e clica em "Iniciar onboarding". O contrato sai na hora pela plataforma de assinatura. Quando o cliente assina às 14h, o webhook avança a esteira sozinho: os acessos nos Sistemas 1 e 2 são criados por API, e a Fernanda recebe uma tarefa com checklist para criar o acesso no Sistema 3 (legado). Ela marca como feito às 14h20, o cliente recebe as credenciais e o Bruno, do comercial, recebe um e-mail dizendo que o cliente está ativo. Se qualquer etapa falhar, a esteira para naquela etapa, a Fernanda é avisada e destrava com um clique, sem reenviar nada que já deu certo. Tudo fica registrado no log de auditoria.

## Audiência principal

Analista de backoffice que conduz de 2 a 10 onboardings por semana, num computador com várias abas abertas, e hoje controla tudo por planilha e e-mail. O comercial é audiência secundária e só consulta.

## Escopo do MVP

1. Formulário de novo onboarding com validação de CNPJ e e-mail.
2. Envio automático do contrato para assinatura digital e avanço automático por webhook quando o cliente assina.
3. Criação automática de acesso nos Sistemas 1 e 2 via API, com até 3 tentativas automáticas em falha técnica.
4. Etapa manual guiada para o Sistema 3 (legado), com checklist e botão "Marcar como feito".
5. Painel com todos os onboardings ativos por status, detalhe com linha do tempo e "Tentar novamente" em etapa com erro.
6. Log de auditoria de toda ação, automática ou humana, e notificação por e-mail (erro para o backoffice, conclusão para o comercial).

## O que NÃO é (pelo menos agora)

- Não é CRM. Não substitui HubSpot, Salesforce ou similar, e não puxa dados deles no MVP.
- Não gerencia contratos: sem renovação, aditivo, versão de minuta ou repositório de contratos.
- Não toca em faturamento nem financeiro.
- Não é acessível pelo cliente final; ele só interage com o e-mail da plataforma de assinatura.
- Não usa IA para decidir nada. Toda etapa é regra fixa ou pessoa (ver `decisoes.md`).
- Não automatiza o Sistema 3 por robô de tela (RPA) nesta versão.

## Critério de sucesso

Em até 60 dias após entrar em produção:
- mediana do tempo interno (do início do onboarding até "concluido", descontada a espera pela assinatura do cliente) abaixo de 2 horas úteis;
- 100% dos novos clientes passando pela ferramenta, com a planilha antiga desativada;
- taxa de onboardings com erro abaixo de 10%.

## Critério de morte

Se em 90 dias após entrar em produção a mediana do tempo interno continuar acima de 1 dia útil, ou se o backoffice ainda mantiver a planilha em paralelo para mais de 30% dos clientes, a ferramenta para de receber funcionalidade nova e o time revisa se o gargalo é o Sistema 3 ou o processo, antes de investir mais.
