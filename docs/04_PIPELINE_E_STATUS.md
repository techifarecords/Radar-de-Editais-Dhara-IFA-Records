# Pipeline operacional de editais

## Status do funil

Valores internos padronizados, sem espaço e sem acento. Nos relatórios, usar o rótulo legível.

| # | Valor interno | Rótulo nos relatórios |
|---:|---|---|
| 1 | `DESCOBERTO` | Descoberto |
| 2 | `EM_VALIDACAO` | Em validação |
| 3 | `AGUARDANDO_REVISAO_HUMANA` | Aguardando revisão humana |
| 4 | `DESCARTADO` | Descartado |
| 5 | `MONITORAR` | Monitorar |
| 6 | `AVALIAR_COM_PARCERIA` | Avaliar com parceria |
| 7 | `APLICAR` | Aplicar |
| 8 | `EM_PREPARACAO` | Em preparação |
| 9 | `PRONTO_PARA_INSCRICAO` | Pronto para inscrição |
| 10 | `INSCRITO` | Inscrito |
| 11 | `RESULTADO_AGUARDADO` | Resultado aguardado |
| 12 | `APROVADO` | Aprovado |
| 13 | `NAO_APROVADO` | Não aprovado |
| 14 | `ENCERRADO` | Encerrado |

Os status 10 a 13 (`INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO`, `NAO_APROVADO`) só podem ser atribuídos com informação humana explícita. As demais transições do funil no Notion seguem os níveis factual e estratégico de `docs/07_NOTION_OPERACAO.md`.

## Status da chamada

Cada oportunidade tem dois campos de status.

### `status_validado` (status original, atribuído pelo `edital-validator`)

Registra o que a fonte oficial diz, inclusive o histórico de alterações.

| Valor interno | Rótulo nos relatórios |
|---|---|
| `ANUNCIADA` | Anunciada |
| `ABERTA` | Aberta |
| `ENCERRADA` | Encerrada |
| `SUSPENSA` | Suspensa |
| `PRORROGADA` | Prorrogada |
| `DESCONHECIDA` | Desconhecida |

`ABERTA` só pode ser usado com evidência atual: prazo futuro inequívoco em fonte oficial, status explícito de inscrições abertas, formulário ou plataforma oficial ativa, ou comunicação oficial recente que confirme inscrições em andamento.

### `status_operacional` (usado para decisões e alertas, atribuído pelo `edital-validator`)

- É `ABERTA` quando `status_validado` for `ABERTA`.
- É `ABERTA` quando `status_validado` for `PRORROGADA` **e** houver, cumulativamente:
  - fonte oficial da prorrogação;
  - novo prazo futuro inequívoco;
  - inscrição disponível ou explicitamente confirmada.
- Nos demais casos, repete o `status_validado`. Uma chamada `PRORROGADA` sem os três requisitos acima tem `status_operacional` = `PRORROGADA` e recebe `REVISAO`.

`PRORROGADA` é um status de histórico e alteração. Quando a chamada prorrogada for tratada como aberta, preservar no registro:

- `status_validado`: `PRORROGADA`;
- `status_operacional`: `ABERTA`;
- data/hora da prorrogação, quando localizada;
- evidência textual e URL da prorrogação.

Nos relatórios, exibir como "Prorrogada — aberta até {{novo prazo}}".

## Decisões analíticas

Valores internos padronizados, atribuídos pelo `dhara-fit-scorer`:

| Decisão | Rótulo nos relatórios | Status do funil correspondente |
|---|---|---|
| `APLICAR` | Aplicar | `APLICAR` |
| `AVALIAR_COM_PARCERIA` | Avaliar com parceria | `AVALIAR_COM_PARCERIA` |
| `MONITORAR` | Monitorar | `MONITORAR` |
| `DESCARTAR` | Descartar | `DESCARTADO` |

As definições de cada decisão estão em `docs/02_CRITERIOS_DE_ELEGIBILIDADE.md` e em `CLAUDE.md`.

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
- `status_validado` e `status_operacional`; em caso de prorrogação, data/hora, URL e evidência da prorrogação.
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

O modelo de registro está em `templates/opportunity-record.md`.

## Prioridades (gatilhos de alerta)

Valores internos padronizados: `URGENTE`, `ALTA_PRIORIDADE`, `REVISAO`. Uma oportunidade pode receber mais de uma prioridade ao mesmo tempo (por exemplo, `URGENTE` e `REVISAO`).

### URGENTE

Exige, cumulativamente, os três critérios abaixo:

- `status_operacional` igual a `ABERTA`, com evidência atual em fonte oficial. Vale para chamadas `ABERTA` e para chamadas `PRORROGADA` que cumpram os requisitos da seção "Status da chamada".
- Decisão `APLICAR` ou `AVALIAR_COM_PARCERIA`.
- Prazo final em até 7 dias corridos a partir da data do relatório.

Se qualquer um dos três critérios não for atendido ou não puder ser confirmado, a oportunidade não é `URGENTE`. Se o horário ou o fuso do prazo for ambíguo, aplicar também `REVISAO`.

### ALTA_PRIORIDADE

Exige, cumulativamente:

- Score igual ou maior que 75.
- `status_operacional` igual a `ABERTA`.
- `confidence_score` igual ou maior que 0,70.

### REVISAO

Aplicar quando houver pelo menos um dos itens:

- Falta de informação crítica.
- Divergência entre página, regulamento e/ou plataforma.
- Dúvida sobre elegibilidade de PJ, CNPJ, sede, certidões, natureza jurídica ou documentação.
- Exigência de parceiro, sede ou residência local, anfitrião, coprodutor ou carta-convite.
- Exigência de visto, idioma ou cofinanciamento.
- Prazo, horário ou timezone ambíguo.
- Chamada `PRORROGADA` sem fonte oficial, prazo futuro inequívoco ou inscrição confirmada.

## Cadência

- Segunda-feira: sincronizar o pipeline no Notion e gravar o log `data/reports/AAAA-MM-DD-sync-notion.md`. Sem relatório. Exceção: havendo `URGENTE` ou alerta crítico (prazo vencido em candidatura em preparação), criar no Notion uma página curta de Tipo "Alerta", só com esses itens, chave `alerta:AAAA-MM-DD`.
- Quinta-feira: sincronizar o pipeline e criar o relatório semanal, cobrindo as rodadas de segunda e quinta da semana. Chave `semanal:AAAA-Www`.
- Rodada manual fora desse calendário: seguir a regra de segunda-feira.
- Revisão mensal: atualização do kit documental e análise de fontes que geram oportunidades relevantes.
