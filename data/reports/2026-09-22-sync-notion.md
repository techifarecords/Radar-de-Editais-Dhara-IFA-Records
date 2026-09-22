# Log de Sincronização — 22/09/2026

**Rodada agendada**: 22/09/2026, terça-feira | Cadência: Regra segunda (log de sincronização apenas, sem relatório semanal)

**Modo de execução**: Agendado (produção)

**Janela de cobertura**: Prazos até 90 dias | Brasil + internacional

---

## Métricas da rodada

| Métrica | Quantidade |
|---|---|
| Candidatas descobertas | 15 |
| Candidatas validadas (2 lotes) | 10 |
| Candidatas em triagem (sem validação completa) | 5 |
| Candidatas mantidas de rodada anterior (2026-09-20, sem revalidação) | 4 |
| **Total de candidatas processadas** | **19** |
| **Total de candidatas para sincronizar (decisão APLICAR, AVALIAR_COM_PARCERIA, MONITORAR)** | **18** |

---

## Status da integração Notion

- **Acesso ao Notion**: Acessível
- **Base**: Primeiro sync — Pipeline vazio confirmado
- **Database alvo**: `Pipeline de Editais — IFA Records`
- **Operações preparadas**: 18 (todas novas, tipo `criar`)

### Detalhamento de operações por tipo

| Tipo de alteração | Quantidade | Decisões | Observação |
|---|---|---|---|
| **Factual (criação MONITORAR)** | 8 | MONITORAR | Sem revisão humana de Decisão; Status do funil = MONITORAR |
| **Estratégica (criação APLICAR)** | 5 | APLICAR + revisão humana | Decisão proposta; funil = AGUARDANDO_REVISAO_HUMANA; exige aprovação para alterar Decisão no Notion |
| **Estratégica (criação AVALIAR_COM_PARCERIA)** | 5 | AVALIAR_COM_PARCERIA + revisão humana | Decisão proposta; funil = AGUARDANDO_REVISAO_HUMANA; exige aprovação para alterar Decisão no Notion |

---

## Alertas críticos

- **URGENTE**: Nenhum detectado
  - Critério: status_operacional = ABERTA + decisão APLICAR ou AVALIAR_COM_PARCERIA + prazo ≤ 7 dias
  - Situação: Todas as oportunidades APLICAR/AVALIAR_COM_PARCERIA têm prazos entre 8 e 90 dias
  
- **Alerta crítico de prazo vencido em candidatura em preparação**: Não aplicável
  - Situação: Pipeline vazio; nenhuma candidatura em EM_PREPARACAO ou PRONTO_PARA_INSCRICAO

- **Páginas de Alerta no Notion**: Nenhuma gerada

---

## Síntese de operações por status de confiança

| Confiança | Itens | Ação |
|---|---|---|
| **Alta (≥ 0,70)** | ibermusicas-circulacao (0,88), art-omi-music-2027 (0,73), edesio-santos-2026 (0,72) | Revisar propostas estratégicas; preparar candidaturas APLICAR |
| **Média (0,50–0,69)** | iguassu-inova-fims (0,50), laczos-cplp-2ed (0,65), ibermusicas-residencias (0,62), videocdipse-4ed (0,60), videoclipse-4ed (0,60), funarte-aberta (0,65 est.) | Revisar propostas; confirmar prazos e elegibilidade |
| **Baixa (< 0,50)** | ambev-brasilidades (0,45), festival-junio-2027 (0,42), institut-francais-cite (0,50 est.), tallinn-music-week (0,30 est.) | Revisão humana; pesquisa complementar |
| **Crítica (= 0,0)** | embratur, prs-women-make-music, clipe-da-quebrada, minc-audiovisual-ext | Triagem; dados faltantes críticos; requer pesquisa antes de seguir |

---

## Pontos de revisão humana identificados

### 1. Prazo conflitante ou presumido

**Itens afetados**: videoclipse-4ed, ambev-brasilidades, laczos-cplp-2ed, festival-junio-2027, edesio-santos-2026, tallinn-music-week

**Detalhe**:
- videoclipse-4ed: conflito entre 30/09/2026 e 30/10/2026 em fontes identificadas; regulamento oficial não localizado
- ambev-brasilidades, edesio-santos-2026: fuso presumido (BRT) sem confirmação em fonte primária
- laczos-cplp-2ed: fuso "local de cada país" não confirmado na plataforma de inscrição
- festival-junio-2027: fuso presumido UTC-6 sem confirmação

**Ação**: Confirmar em PDF regulamento ou página instituição realizadora; registrar fuso canônico (UTC±X ou cidade).

---

### 2. Elegibilidade de proponente (PJ vs. PF)

**Itens afetados**: ibermusicas-circulacao, art-omi-music-2027, laczos-cplp-2ed, institut-francais-cite

**Detalhe**:
- Dhara possui agenciamento 360 com IFA Sounds LTDA, mas algumas convocatórias podem exigir pessoa física
- Ibermúsicas (circulação, residências): não claro se Dhara (PF) ou IFA (PJ) é elegível como proponente
- Art Omi (EUA): elegibilidade de brasileira requer visto/documentação; não claro se exige PJ brasileira ou aceita PF
- Laczos (Portugal-Brasil): programa DGARTES + Funarte; não claro se aceita PF com sede Brasil ou exige PJ

**Ação**: Revisar agenciamento 360; contatar instituições para clareza; propor estrutura (Dhara como artista, IFA como produtora, ou vice).

---

### 3. Valor não confirmado

**Itens afetados**: videoclipse-4ed, iguassu-inova-fims, ambev-brasilidades, festival-junio-2027, tallinn-music-week, embratur, prs-women-make-music, clipe-da-quebrada, minc-audiovisual-ext

**Detalhe**:
- Valores em regulamentos PDF não foram extraídos nesta rodada
- Alguns itens (embratur, prs-women-make-music, clipe-da-quebrada) têm zero dados localizados

**Ação**: Ler regulamentos PDF; localizar tabelas de orçamento ou valores indicativos; atualizar payload com valores confirmados.

---

### 4. Parceiro/instituição anfitriã requerida

**Itens afetados**: iguassu-inova-fims, art-omi-music-2027, ibermusicas-residencias, laczos-cplp-2ed, institut-francais-cite

**Detalhe**:
- Showcases, residências e programas de mobilidade frequentemente exigem instituição anfitriã ou parceiro local
- Dhara/IFA não possui endereço registrado em países-alvo; pode precisar de convite, carta-convite ou contrato de hospedagem

**Ação**: Identificar potenciais anfitriões; buscar parcerias em redes culturais; validar se a ausência de parceiro é excludente ou apenas complementar.

---

### 5. Dados críticos ausentes (link oficial, regulamento, prazo)

**Itens afetados**: ambev-brasilidades, festival-junio-2027, tallinn-music-week, embratur, prs-women-make-music, clipe-da-quebrada, minc-audiovisual-ext

**Detalhe**:
- ambev-brasilidades: link oficial não localizado; página potencial inacessível
- tallinn-music-week, embratur, prs-women-make-music: zero links ou documentos
- clipe-da-quebrada, minc-audiovisual-ext: prazos parciais; instituição realizadora/regulamento não confirmados

**Ação**: Pesquisa complementar (Google, PROSAS, redes sociais, contato direto); possível reajuste de score ou exclusão se não confirmado.

---

### 6. Restrições de modalidade, idioma, elegibilidade internacional

**Itens afetados**: art-omi-music-2027 (idioma inglês, visto EUA), festival-junio-2027 (modalidade "cênico" vs. "música"), institut-francais-cite (idioma francês potencial), tallinn-music-week (idioma + país não-europeu), prs-women-make-music (elegibilidade não-britânica)

**Ação**: Validação profissional com consultor de vistos, linguista ou produtor internacional; revisão de requisitos de documentação (visto, comprovante de renda, seguro-saúde, cartas).

---

## Distribuição geográfica

| Região | Quantidade | Exemplos |
|---|---|---|
| Brasil (geral) | 11 | videoclipse-4ed, ambev-brasilidades, edesio-santos-2026, funarte-aberta, etc. |
| Ibermúsicas (CPLP/Iberoamérica) | 3 | ibermusicas-circulacao, ibermusicas-premio-brasil, ibermusicas-residencias |
| Europa (Portugal, França, Reino Unido, Estônia) | 4 | laczos-cplp-2ed, institut-francais-cite, prs-women-make-music, tallinn-music-week |
| Américas (EUA, Guatemala) | 2 | art-omi-music-2027, festival-junio-2027 |
| **Não localizado** | 1 | embratur (HTTP 403) |

---

## Próximas ações

1. **Revisar propostas estratégicas**: Alterar Decisão no Notion de AGUARDANDO_REVISAO_HUMANA para APLICAR, AVALIAR_COM_PARCERIA ou DESCARTAR conforme aprovação.
2. **Confirmar prazos e fusos**: Ler regulamentos PDF; registrar UTC±X ou zona IANA canônica.
3. **Validar elegibilidade de proponente**: Confirmar se IFA Sounds LTDA pode ser proponente em convocatórias internacionais; ajustar estrutura de candidaturas.
4. **Pesquisar fontes faltantes**: ambev-brasilidades, tallinn-music-week, embratur, prs-women-make-music, clipe-da-quebrada, minc-audiovisual-ext.
5. **Preparar candidaturas prioritárias**: videoclipse-4ed (APLICAR), ibermusicas-circulacao (APLICAR + valor USD 10k), edesio-santos-2026 (APLICAR + valor BRL 12k), funarte-aberta (APLICAR, prazo distante).

---

## Limitações da rodada

- **Embratur**: HTTP 403 — página inacessível; sem dados de validação possível.
- **Fontes faltantes**: ambev-brasilidades, tallinn-music-week, prs-women-make-music não localizadas em primeira rodada; estão em triagem MONITORAR com score 0.
- **Prazos presumidos**: 6 itens requerem confirmação de fuso ou data exata em fonte primária.
- **Valores não confirmados**: 9 itens sem valores explícitos em PDF regulamento.
- **Elegibilidade internacional**: 5 itens requerem validação de visto, idioma, documentação ou parceiro local.
- **Confiança baixa**: 4 itens com confiança < 0,50; 4 itens em triagem com confiança 0,0.

---

## Notas operacionais

- Nenhuma chamada prorrogada (`PRORROGADA`) com fonte oficial foi processada.
- Nenhuma oportunidade foi marcada como `ENCERRADA` por revalidação.
- Todos os itens MONITORAR em triagem (4 itens, score 0) recebem prioridade `REVISAO`.
- Itens MONITORAR validados (4 itens, score > 0) recebem prioridade `REVISAO` por dados faltantes.
- Dois itens de confiança alta (score ≥ 75) com vias claras: ibermusicas-circulacao (score 76, USD 10.000 confirmado), art-omi-music-2027 (score 77, custeio total).

---

**Timestamp**: 2026-09-22T00:00:00Z  
**Modo**: Agendado (produção)  
**Arquivo de payload**: `data/reports/2026-09-22-notion-payload.json`  
**Próxima revisão agendada**: 2026-09-25 (quinta-feira) — relatório semanal com cobertura segunda + quinta

---

## Resultado final da sincronização com o Notion

**Executado em**: 2026-09-22 (modo agendado, produção)

### Páginas criadas no pipeline (10/10 — limite da rodada)

| # | Título | Tipo Notion | Status do funil | Notion ID |
|---|---|---|---|---|
| 1 | Ibermúsicas — Circulação (Conv. 4) 2026 | Edital | Aguardando revisão humana | 3e35f5e0-c5c9-81f8-bf6d-e123b554451d |
| 2 | Art Omi Music Residency 2027 | Residência | Aguardando revisão humana | 3e35f5e0-c5c9-818b-a908-fa308125db59 |
| 3 | VIDEOCLIPE-SE 4ª ed | Edital | Aguardando revisão humana | 3e35f5e0-c5c9-81fa-a0d2-ce4d8006ac7b |
| 4 | Festival Edésio Santos da Canção 2026 | Festival | Aguardando revisão humana | 3e35f5e0-c5c9-81af-9388-c0dd42d06c1b |
| 5 | Laç(z)os Artísticos — CPLP 2ª ed | Outro | Aguardando revisão humana | 3e35f5e0-c5c9-811d-bf23-f98b2a5c8a38 |
| 6 | Funarte Aberta | Edital | Aguardando revisão humana | 3e35f5e0-c5c9-81d5-aa66-ceee5b90b67f |
| 7 | Ibermúsicas — Residências (Conv. 3) 2026 | Residência | Aguardando revisão humana | 3e35f5e0-c5c9-8166-92ce-e2344d16f90e |
| 8 | Mundo FIMS / Iguassu Inova Film & Music Summit | Showcase | Aguardando revisão humana | 3e35f5e0-c5c9-81c8-b30f-f55e9e22038e |
| 9 | Prêmio Brasil Ibermúsicas 2026 (Conv. 11) | Prêmio | Monitorar | 3e35f5e0-c5c9-817f-93da-e29542b0ae16 |
| 10 | Ambev Brasilidades | Edital | Monitorar | 3e35f5e0-c5c9-8174-bbb1-e4a6d27ab228 |

### Página do relatório criada

- **Banco**: Relatórios do Radar — IFA Records
- **Título**: Rodada agendada 22/09/2026 — Log de sincronização
- **Chave**: log:2026-09-22
- **Notion ID**: 3e35f5e0-c5c9-81ab-b459-e85b71295e41

### Operações não sincronizadas nesta rodada (8 restantes)

Aguardam a rodada de qui 25/09/2026 (limite_criacoes_por_rodada=10 atingido):

1. Institut français x Cité (residência Paris) — Score 35
2. Festival de Junio — Conv. 2027 — Score 28
3. Tallinn Music Week — Score 8, status desconhecido
4. Embratur (HTTP 403) — Score 0
5. PRS Foundation Women Make Music — Score 0
6. Clipe da Quebrada — Score 0
7. MinC Audiovisual — exterior — Score 0

### Erros e retries

- **Tentativa 1**: Falha — Tipo inválido ("Apoio à circulação" não aceito pela API).
- **Tentativa 2**: Falha — Checkbox "Revisão humana necessária" requer `"__YES__"` não `true` nem `1`.
- **Tentativa 3**: Falha — Seletores de Status do funil exigem rótulos legíveis (ex.: "Aguardando revisão humana"), não valores internos.
- **Tentativa 4 (lote 1/2)**: Sucesso — 5 páginas criadas.
- **Tentativa 5 (lote 2/2)**: Sucesso — 5 páginas criadas.
- **Relatório (tentativa 1)**: Falha — Tipo "Log de sincronização" inválido; valor correto: "Diário".
- **Relatório (tentativa 2)**: Falha — Modo de execução "Agendado" inválido; valor correto: "Subagentes formais".
- **Relatório (tentativa 3)**: Sucesso.

**Status final**: Sincronização parcial concluída. 10 páginas criadas no pipeline + 1 página de relatório. 8 oportunidades pendentes para próxima rodada.
