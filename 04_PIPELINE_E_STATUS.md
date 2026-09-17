# Pipeline operacional de editais

## Status do funil

1. DESCOBERTO
2. EM_VALIDAÇÃO
3. AGUARDANDO_REVISÃO_HUMANA
4. DESCARTADO
5. MONITORAR
6. AVALIAR_COM_PARCERIA
7. APLICAR
8. EM_PREPARAÇÃO
9. PRONTO_PARA_INSCRIÇÃO
10. INSCRITO
11. RESULTADO_AGUARDADO
12. APROVADO
13. NÃO_APROVADO
14. ENCERRADO

## Dados obrigatórios

- Nome do edital.
- Instituição realizadora.
- País, estado/província, cidade e abrangência.
- Tipo: edital, prêmio, residência, festival, showcase, contratação, intercâmbio etc.
- Linguagem cultural.
- Link oficial.
- Link para inscrição.
- Link para regulamento/PDF.
- Prazo, hora e fuso.
- Valor e moeda.
- Número estimado de selecionados, se informado.
- Elegibilidade para PF, PJ, coletivo e outras categorias.
- Requisitos de CNPJ, sede, residência, nacionalidade, tempo de atuação e documentos.
- Escopo financiável e itens vedados.
- Contrapartidas, critérios de seleção e etapas.
- Score.
- Decisão.
- Nível de confiança.
- Riscos e pendências.
- Próxima ação.
- Evidência textual e data de validação.

## Gatilhos

URGENTE:
- Prazo de até 7 dias.
- Decisão APLICAR ou AVALIAR_COM_PARCERIA.

ALTA PRIORIDADE:
- Score igual ou maior que 75.
- Status aberto confirmado.
- Confiança igual ou maior que 0,70.

REVISÃO:
- Falta de informação crítica.
- Divergência entre página e regulamento.
- Dúvida sobre elegibilidade de PJ.
- Exigência de parceiro, sede ou residência local.
- Prazo ou timezone ambíguo.

## Cadência

- Rodada diária: descoberta, validação e alertas.
- Revisão semanal: priorização, decisões e atualização do funil.
- Revisão mensal: atualização do kit documental e análise de fontes que geram oportunidades relevantes.
