# Relatório semanal — Radar de Editais Dhara / IFA Records

<!--
Modelo usado pelo edital-reporter.
Gravar em: data/reports/AAAA-Www-semanal.md (semana ISO; sufixo -r2, -r3 se já existir).
Inclui o consolidado dos relatórios diários da semana.
Não inventar dados: usar "não localizado" ou "não informado".
Exibir rótulos legíveis (ex.: "Avaliar com parceria", "Pronto para inscrição"), não os valores internos.
-->

- **Semana:** {{AAAA-Www}} ({{AAAA-MM-DD}} a {{AAAA-MM-DD}})
- **Relatórios diários consolidados:** {{lista de arquivos em data/reports/}}
- **Modo de execução predominante:** {{subagentes_formais | modo_agente_unico}}

## 1. Resumo da semana

| Indicador | Quantidade |
|---|---:|
| Fontes processadas | {{n}} |
| Candidatas descobertas | {{n}} |
| Validadas | {{n}} |
| Descartadas | {{n}} |
| `URGENTE` | {{n}} |
| `ALTA_PRIORIDADE` | {{n}} |
| `REVISAO` | {{n}} |

## 2. Pipeline por decisão

| Decisão | Quantidade | Oportunidades |
|---|---:|---|
| `APLICAR` | {{n}} | {{títulos}} |
| `AVALIAR_COM_PARCERIA` | {{n}} | {{títulos}} |
| `MONITORAR` | {{n}} | {{títulos}} |
| `DESCARTAR` | {{n}} | {{títulos}} |

## 3. Ranking das 10 oportunidades mais relevantes

| # | Título | Instituição | Território | Score | Decisão | Prioridade | Confiança | Prazo (data, hora, fuso) | Próxima ação |
|---:|---|---|---|---:|---|---|---:|---|---|
| 1 | {{título}} | {{instituição}} | {{território}} | {{score}} | {{decisão}} | {{prioridades}} | {{conf.}} | {{prazo}} | {{ação}} |

## 4. Calendário dos próximos 30 dias

Ordenado por prazo.

| Prazo (data, hora, fuso) | Oportunidade | Decisão | Etapa | Responsável |
|---|---|---|---|---|
| {{prazo}} | {{título}} | {{decisão}} | {{inscrição / envio de documento / resultado}} | {{a definir}} |

## 5. Oportunidades brasileiras

| Título | Instituição | UF / cidade | Modalidade | Valor e moeda | Prazo | Score | Decisão | Maior risco | Próxima ação | Link oficial |
|---|---|---|---|---|---|---:|---|---|---|---|
| {{título}} | {{instituição}} | {{UF / cidade}} | {{modalidade}} | {{valor}} | {{prazo}} | {{score}} | {{decisão}} | {{risco}} | {{ação}} | {{url}} |

## 6. Oportunidades internacionais

| Título | Instituição | País | Idioma | Parceiro / anfitrião | Mobilidade | Visto | Custos não cobertos | Cofinanciamento | Prazo | Score | Decisão | Link oficial |
|---|---|---|---|---|---|---|---|---|---|---:|---|---|
| {{título}} | {{instituição}} | {{país}} | {{idioma}} | {{exigência ou não informado}} | {{cobre viagem? ou não informado}} | {{exigência ou não informado}} | {{lista ou não informado}} | {{exigência ou não informado}} | {{prazo}} | {{score}} | {{decisão}} | {{url}} |

## 7. Checklist documental consolidado

Baseado em `docs/05_KIT_DOCUMENTAL.md`. Registrar apenas disponibilidade, nunca o conteúdo dos documentos.

### Dhara

| Documento | Pedido por | Disponível? | Observação |
|---|---|---|---|
| {{documento}} | {{oportunidades}} | {{sim / não / verificar}} | {{obs.}} |

### IFA Sounds / IFA Records

| Documento | Pedido por | Disponível? | Observação |
|---|---|---|---|
| {{documento}} | {{oportunidades}} | {{sim / não / verificar}} | {{obs.}} |

## 8. Padrões observados

- **Fontes que mais geraram oportunidades:** {{lista}}
- **Exigências recorrentes:** {{lista}}
- **Lacunas a preparar no kit de inscrição:** {{lista}}

## 9. Propostas de atualização de fontes acumuladas

Consolidado das propostas dos relatórios diários. **Não validadas**; `config/sources.yaml` só muda com aprovação humana.

| Fonte (`id`) | URL sugerida | Evidência | Vezes sugerida na semana | Situação |
|---|---|---|---:|---|
| {{id}} | {{url}} | {{trecho curto}} | {{n}} | Proposta — requer validação humana |

## 10. Sincronização com o Notion

| Rodada | Situação | Criadas | Factuais gravadas | Estratégicas aprovadas | Estratégicas recusadas ou adiadas | Bloqueadas | Falhas | Log |
|---|---|---:|---:|---:|---:|---:|---:|---|
| {{AAAA-MM-DD}} | {{Concluída / Parcial / Falhou / Não realizada}} | {{n}} | {{n}} | {{n}} | {{n}} | {{n}} | {{n}} | `{{data/reports/AAAA-MM-DD-sync-notion.md}}` |

- **Prazo vencido em candidatura em preparação:** {{lista de oportunidades com proposta aberta ou "nenhuma"}}
- **Operações pendentes:** {{lista ou "nenhuma"}}
- **Possíveis duplicatas detectadas (não gravadas):** {{lista ou "nenhuma"}}

## 11. Limitações da semana

- {{Fontes inacessíveis, cobertura parcial, erros de coleta}}

## Decisões humanas necessárias

- {{Somente decisões que dependem da usuária ou da IFA}}
