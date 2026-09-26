# Log de Sincronização com o Notion — 2026-09-26

**Data/hora:** 2026-09-26 (modo agendado — Saturday, cadência de segunda-feira)
**Banco de dados alvo:** producao
**Pipeline:** `37958932-449b-4375-91b1-1476130fa02f` (data_source: `be0fccbf-ce43-4daa-ba66-0d7d7657ca8c`)
**Relatórios:** `d50929f2-d9f1-439c-8fbf-b67fb7e92c2a` (data_source: `cc1b9a23-1e56-47bd-8d20-a68a3e96209c`)
**Schema verificado:** sim (config/notion.yaml `schema_verificado: true`, verificado_em: 2026-09-21)
**Modo agendado:** habilitado | alvo: producao | sem_limite: true

---

## Resultado: CONCLUÍDA

---

## Operações Factuais (gravadas diretamente)

### 1. Atualização — Formemus Rodadas de Negócios (prazo vencido)

- **Página:** `3e45f5e0-c5c9-813c-b560-d21ff9ddb7e0`
- **URL Notion:** https://app.notion.com/p/3e45f5e0c5c9813cb560d21ff9ddb7e0
- **Chave de deduplicação:** `id:formemus-rodadas-negocios-2026:3e45f5e0`
- **Gatilho:** Prazo final 2026-09-24 vencido sem prorrogação oficial; status_operacional ENCERRADA
- **Status do funil antes:** Monitorar (não estava em EM_PREPARACAO/PRONTO_PARA_INSCRICAO)
- **Campos alterados:**
  - Status validado: Desconhecida → Encerrada
  - Status operacional: Aberta → Encerrada
  - Status do funil: Monitorar → Encerrado
  - Última validação: → 2026-09-26
  - Histórico de alterações: acréscimo (encerramento por prazo vencido)
- **Resultado:** ✅ OK

### 2. Criação — Espace Brownstone LATAM 2027 (MONITORAR — factual)

- **Página criada:** `3e75f5e0-c5c9-8179-a6e8-c2cf55eb9630`
- **URL Notion:** https://app.notion.com/p/3e75f5e0c5c98179a6e8c2cf55eb9630
- **Chave de deduplicação:** `https://www.artinlatam.com/p/open-call-espace-brownstone-art-in`
- **Decisão:** Monitorar | **Status do funil:** Monitorar
- **Score:** 37 | **Confiança:** 0,52
- **Prazo final:** 2026-10-15 (CEST 23:59)
- **Resultado:** ✅ OK

---

## Propostas Estratégicas (modo agendado — aguardam aprovação humana no Notion)

Em modo agendado, as operações estratégicas NÃO alteram "Decisão" nem "Status do funil" diretamente.
Foram gravadas em "Decisão proposta" + "Proposta estratégica" + "Revisão humana necessária = true".
A pessoa usuária aprova alterando o campo "Decisão" diretamente no Notion.

### 3. Criação — Ibermúsicas Especialização 2026 ⚠️ URGENTE

- **Página criada:** `3e75f5e0-c5c9-8155-a634-d319754a580e`
- **URL Notion:** https://app.notion.com/p/3e75f5e0c5c98155a634d319754a580e
- **Chave de deduplicação:** `https://www.gov.br/funarte/pt-br/editais/2026/programa-ibermusicas-convocatorias-2026/apoio-a-especializacao-e-ao-aperfeicoamento-artistico-e-tecnico`
- **Decisão proposta:** Aplicar | **Status do funil:** Aguardando revisão humana
- **Prioridade:** Urgente, Revisão
- **Score:** 70 | **Confiança:** 0,87
- **Prazo final:** 2026-10-01 (5 dias — URGENTE)
- **Resultado:** ✅ OK (aguarda aprovação humana)

### 4. Criação — Ibermúsicas Emilia-Romagna 2026

- **Página criada:** `3e75f5e0-c5c9-8190-8040-df5c9876ffbb`
- **URL Notion:** https://app.notion.com/p/3e75f5e0c5c981908040df5c9876ffbb
- **Chave de deduplicação:** `https://www.ibermusicas.org/index.php/o-prazo-para-inscricao-na-convocatoria-especial-ibermusicas-emilia-romagna-conectando-artistas-e-cenas-musicais-foi-prorrogado-ate-21-de-outubro/`
- **Decisão proposta:** Avaliar com parceria | **Status do funil:** Aguardando revisão humana
- **Score:** 64 | **Confiança:** 0,72
- **Prazo final:** 2026-10-21
- **Resultado:** ✅ OK (aguarda aprovação humana)

### 5. Criação — Residência IF × Cité des Arts 2027-2028

- **Página criada:** `3e75f5e0-c5c9-813e-afae-c8dd68020ca5`
- **URL Notion:** https://app.notion.com/p/3e75f5e0c5c9813eafaec8dd68020ca5
- **Chave de deduplicação:** `https://www.institutfrancais.com/en/programme/residence-and-professional-mobility/residencies-institut-francais-x-cite-internationale`
- **Decisão proposta:** Avaliar com parceria | **Status do funil:** Aguardando revisão humana
- **Score:** 58 | **Confiança:** 0,74
- **Prazo final:** 2026-10-08 (12 dias — requer contato urgente com parceiro)
- **Resultado:** ✅ OK (aguarda aprovação humana)

### 6. Criação — Art Explora Cité des Arts 2027 ⭐ ALTA PRIORIDADE

- **Página criada:** `3e75f5e0-c5c9-818f-9bf7-ee85fab0e503`
- **URL Notion:** https://app.notion.com/p/3e75f5e0c5c9818f9bf7ee85fab0e503
- **Chave de deduplicação:** `https://www.artexplora.org/en/the-artists-residencies-programme-presentation`
- **Decisão proposta:** Avaliar com parceria | **Status do funil:** Aguardando revisão humana
- **Prioridade:** Alta prioridade, Revisão
- **Score:** 75 | **Confiança:** 0,78
- **Prazo final:** 2026-10-30
- **Resultado:** ✅ OK (aguarda aprovação humana)

### 7. Criação — Tallinn Music Week 2027

- **Página criada:** `3e75f5e0-c5c9-81ad-bc61-c18314138e89`
- **URL Notion:** https://app.notion.com/p/3e75f5e0c5c981adbc61c18314138e89
- **Chave de deduplicação:** `descoberta:https://tmw.ee/artist-applications`
- **Decisão proposta:** Avaliar com parceria | **Status do funil:** Aguardando revisão humana
- **Score:** 55 | **Confiança:** 0,62
- **Prazo final:** 2026-10-26
- **Resultado:** ✅ OK (aguarda aprovação humana)

### 8. Criação — SXSW 2027

- **Página criada:** `3e75f5e0-c5c9-8199-8b0e-f2a07a1a6714`
- **URL Notion:** https://app.notion.com/p/3e75f5e0c5c981998b0ef2a07a1a6714
- **Chave de deduplicação:** `descoberta:https://sxsw.com/apply/showcase-applications/`
- **Decisão proposta:** Avaliar com parceria | **Status do funil:** Aguardando revisão humana
- **Score:** 48 | **Confiança:** 0,63
- **Prazo final:** 2026-11-20
- **Resultado:** ✅ OK (aguarda aprovação humana)

---

## Página de Alerta criada no Notion

- **Título:** Alerta 2026-09-26
- **Chave:** `alerta:2026-09-26`
- **Tipo:** Alerta
- **Página:** `3e75f5e0-c5c9-8159-ab4f-d2827df433c4`
- **URL Notion:** https://app.notion.com/p/3e75f5e0c5c98159ab4fd2827df433c4
- **Oportunidades linkadas:** 8 (7 novas + Formemus)
- **Decisões humanas pendentes:** sim

---

## Operações Bloqueadas / Encerradas sem gravação

Nenhuma.

---

## Resumo

| Categoria | Quantidade |
|---|---|
| Atualizações factuais | 1 (Formemus encerrado) |
| Criações factuais (MONITORAR) | 1 (Brownstone) |
| Propostas estratégicas gravadas | 6 (aguardam aprovação) |
| Página de alerta criada | 1 |
| Operações bloqueadas | 0 |
| Falhas | 0 |

---

## Arquivos locais desta rodada

- `data/reports/2026-09-26-relatorio-rodada.md` — relatório completo da rodada
- `data/reports/2026-09-26-notion-payload.json` — payload gerado pelo edital-reporter
- `data/reports/2026-09-26-sync-notion.md` — este log de sincronização
