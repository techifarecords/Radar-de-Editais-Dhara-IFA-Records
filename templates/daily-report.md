# Relatório diário — Radar de Editais Dhara / IFA Records

<!--
Modelo usado pelo edital-reporter.
Gravar em: data/reports/AAAA-MM-DD-diario.md (sufixo -r2, -r3 se já existir).
Substituir {{campos}}. Não inventar dados: usar "não localizado" ou "não informado".
Exibir rótulos legíveis (ex.: "Avaliar com parceria", "Em validação"), não os valores internos.
Chamada prorrogada tratada como aberta: "Prorrogada — aberta até {{novo prazo}}".
Remover as linhas de "Nenhum item" quando a seção tiver itens.
-->

- **Data do relatório:** {{AAAA-MM-DD}}
- **Janela de coleta:** {{data/hora início}} a {{data/hora fim}} ({{fuso}})
- **Modo de execução:** {{subagentes_formais | modo_agente_unico}}
- **Escopo:** {{Brasil e exterior | outro escopo definido}}
- **Cobertura:** {{Brasil | Internacional | Brasil e internacional}}
- **Notion:** {{acessível | inacessível | não configurado}}

## 1. Resumo executivo

| Indicador | Quantidade |
|---|---:|
| Fontes processadas | {{n}} |
| Candidatas descobertas | {{n}} |
| Validadas | {{n}} |
| Descartadas | {{n}} |
| `URGENTE` | {{n}} |
| `ALTA_PRIORIDADE` | {{n}} |
| `REVISAO` | {{n}} |

{{Síntese em 2 ou 3 frases.}}

## 2. Urgentes

Critério: `status_operacional` = `ABERTA` (inclui prorrogada confirmada) + decisão `APLICAR` ou `AVALIAR_COM_PARCERIA` + prazo em até 7 dias. Ordenado por prazo.

| Título | Instituição | País / território | Modalidade | Valor e moeda | Prazo (data, hora, fuso) | Score | Decisão | Confiança | Motivo de aderência | Maior risco | Próxima ação | Link oficial | Regulamento |
|---|---|---|---|---|---|---:|---|---:|---|---|---|---|---|
| {{título}} | {{instituição}} | {{país / UF / cidade}} | {{modalidade}} | {{valor moeda ou não localizado}} | {{prazo}} | {{0-100}} | {{decisão}} | {{0,00}} | {{motivo}} | {{risco}} | {{ação}} | {{url}} | {{url}} |

_Nenhum item urgente nesta rodada._

## 2b. Prazo vencido em candidatura em preparação

Alerta crítico. Oportunidades em "Em preparação" ou "Pronto para inscrição" com edital encerrado ou prazo vencido. Os campos factuais já foram atualizados; funil e Decisão aguardam decisão humana.

| Oportunidade | Status do funil atual | Decisão atual | Prazo original | Detectado em | Evidência | URL | Impacto operacional | Proposta |
|---|---|---|---|---|---|---|---|---|
| {{título}} | {{Em preparação / Pronto para inscrição}} | {{decisão}} | {{prazo}} | {{AAAA-MM-DD HH:MM}} | {{trecho curto}} | {{url}} | {{impacto}} | {{Descartado + Descartar / Manter por motivo excepcional / Outro}} |

_Nenhum caso nesta rodada._

## 3. Novas oportunidades prioritárias (score ≥ 60)

Ordenadas por score e, em seguida, por prazo. Marcar `ALTA_PRIORIDADE` quando score ≥ 75, `status_operacional` = `ABERTA` e confiança ≥ 0,70.

| Título | Instituição | País / território | Modalidade | Valor e moeda | Prazo (data, hora, fuso) | Score | Decisão | Prioridade | Confiança | Motivo de aderência | Maior risco | Próxima ação | Link oficial | Regulamento |
|---|---|---|---|---|---|---:|---|---|---:|---|---|---|---|---|
| {{título}} | {{instituição}} | {{território}} | {{modalidade}} | {{valor}} | {{prazo}} | {{score}} | {{decisão}} | {{prioridades}} | {{conf.}} | {{motivo}} | {{risco}} | {{ação}} | {{url}} | {{url}} |

_Nenhuma nova oportunidade prioritária nesta rodada._

## 4. Atualizações

Mudanças de prazo, status, regulamento, valor ou elegibilidade em oportunidades já conhecidas.

| Oportunidade | Campo alterado | Antes | Depois | Fonte da mudança | Data da validação |
|---|---|---|---|---|---|
| {{título}} | {{campo}} | {{valor anterior}} | {{valor novo}} | {{url}} | {{AAAA-MM-DD HH:MM}} |

_Nenhuma atualização nesta rodada._

## 5. Revisão humana necessária

| Oportunidade | Ponto de decisão ou informação faltante | Motivo (`REVISAO`) | Fonte |
|---|---|---|---|
| {{título}} | {{o que precisa ser decidido ou confirmado}} | {{campo ausente / conflito / elegibilidade PJ / parceiro / visto / fuso}} | {{url}} |

## 6. Próximas ações

No máximo cinco, cada uma iniciando com verbo.

1. {{Verbo + ação}}

## 7. Limitações da rodada

- **Fontes inacessíveis:** {{lista ou "nenhuma"}}
- **Prazos não confirmados:** {{lista ou "nenhum"}}
- **Cobertura parcial:** {{territórios, idiomas ou fontes não cobertos}}
- **Erros de coleta:** {{descrição ou "nenhum"}}
- **Sincronização com o Notion:** {{sem falhas | descrição da falha}}

## 8. Propostas de atualização de fontes

URLs sugeridas para fontes com `url: null` em `config/sources.yaml`. **Não validadas.** O arquivo de configuração não é alterado automaticamente.

| Fonte (`id`) | Nome | URL sugerida | Onde foi encontrada | Evidência de que é oficial | Situação |
|---|---|---|---|---|---|
| {{id}} | {{nome}} | {{url}} | {{busca / página de origem}} | {{trecho curto}} | Proposta — requer validação humana |

_Nenhuma proposta nesta rodada._

## 9. Sincronização com o Notion

Preenchido pelo `edital-reporter` antes da gravação. O resultado final fica no log da sessão principal.

- **Situação:** {{habilitada | não configurada | inacessível}}
- **Operações preparadas:** {{n}} oportunidades ({{n}} para avaliar criação, {{n}} para avaliar atualização) e 1 página de relatório
- **Por nível:** {{n}} factuais; {{n}} estratégicas, que dependem de aprovação e estão listadas em "Decisões humanas necessárias"
- **Payload:** `{{data/reports/AAAA-MM-DD-notion-payload.json | não gerado}}`
- **Log de sincronização:** `data/reports/{{AAAA-MM-DD}}-sync-notion.md`
- **Pendências de rodadas anteriores:** {{lista ou "nenhuma"}}

## Decisões humanas necessárias

- {{Somente decisões que dependem da usuária ou da IFA}}
- {{Propostas estratégicas para o Notion: oportunidade, valor atual → valor proposto, motivo}}
