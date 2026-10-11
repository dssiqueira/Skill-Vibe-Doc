# Manutenção: atualizar e revisar

## Mudou isso → atualize aquilo

| Mudança no projeto | Arquivos |
|---|---|
| Nova tabela, coluna, relação ou regra de validação | `estruturadedados.md` (e `fluxos.md` se aparece na tela) |
| Nova tela, rota, modal ou passo de fluxo | `fluxos.md` (e `metricas.md` se gera evento) |
| Cor, fonte, espaçamento, raio, sombra ou componente novo | `DESIGN.md` |
| Nova API, serviço, chave de ambiente, provedor de login ou pagamento | `integracoes.md` e `decisoes.md` |
| Troca de biblioteca, banco, framework ou modelo de IA | `decisoes.md` e `integracoes.md` |
| Novo evento de analytics ou métrica | `metricas.md` |
| Mudança de escopo, público ou prioridade | `contexto.md` e, se for o caso, `personas.md` |
| Comando novo para rodar, testar ou publicar | `AGENTS.md` |
| Entrega que bateu ou não bateu o critério de sucesso | `contexto.md` (registre o resultado com data) |

## Critérios de revisão, do mais grave ao menos

1. **Contradição entre arquivos.** Duas fontes dizendo coisas diferentes fazem a IA escolher uma no chute.
2. **Docs atrás do código.** Procure no código: tabelas e modelos (migrations, schema, ORM), rotas e páginas, variáveis de cor e fonte (CSS, Tailwind config, tema), integrações (SDKs no package.json, variáveis de ambiente). Tudo que existe no código e não está nos docs é dívida.
3. **Vago que obriga a chutar.** Sinais: "moderno", "intuitivo", "usuários em geral", "engajamento", "escalável", "boa performance" sem número.
4. **Faltando o que não é.** `contexto.md` sem escopo negativo.
5. **Sem régua.** `contexto.md` sem critério de sucesso ou de morte com número e prazo.
6. **Texto de exemplo esquecido.** Restos do template, nomes de exemplo, TODO.
7. **DESIGN.md inválido.** Seções fora de ordem, referência quebrada, contraste abaixo de 4,5:1.

## Formato da resposta de revisão

```
1. [docs/fluxos.md] A tela "Relatórios" está no código (app/relatorios) e não aparece aqui.
   Correção: acrescentar a tela com objetivo, hierarquia e o fluxo de exportar.
2. ...
```

Termine com uma linha: quantos itens graves (1 e 2) e quantos ajustes (3 a 7).
