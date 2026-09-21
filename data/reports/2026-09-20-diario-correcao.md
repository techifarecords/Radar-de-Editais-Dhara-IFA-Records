# Relatório diário — Radar de Editais Dhara / IFA Records (correção)

> **Nota de correção:** esta versão corrige exclusivamente o tratamento do prazo e da decisão do **VIDEOCLIPE-SE Festival — 4ª edição** no relatório `data/reports/2026-09-20-diario.md`. O relatório original é preservado sem alteração, para rastreabilidade. Nenhum outro dado, evidência, score ou conclusão de subagente foi alterado nesta correção.
>
> **Motivo da correção:** o regulamento oficial do VIDEOCLIPE-SE traz duas datas conflitantes para o encerramento das inscrições — item 3.1: 30/09/2026; cronograma do item 8: 30/10/2026 — sem indicação de qual prevalece. O relatório original tratava 30/09 como "prazo operacional" sem que essa escolha estivesse baseada em evidência (era uma inferência). Nesta correção, as duas datas são registradas como conflito de fonte, sem inferir qual é a correta; o item permanece em `REVISAO` até confirmação oficial por escrito da organização; e a decisão foi reavaliada porque dependia da data inferida.

- **Data do relatório:** 2026-09-20
- **Janela de coleta:** 2026-09-20 — hora de início e de fim não registradas (as ferramentas de busca não retornam carimbo de hora) (America/Sao_Paulo)
- **Modo de execução:** `subagentes_formais`
- **Escopo:** Brasil e exterior — chamadas abertas ou anunciadas com prazo nos próximos 90 dias (até 2026-12-19). Limite piloto: máx. 12 candidatas descobertas e máx. 8 validadas
- **Cobertura:** Brasil e internacional
- **Notion:** não configurado

## 1. Resumo executivo

| Indicador | Quantidade |
|---|---:|
| Fontes processadas | 12 tocadas (11 com resultado útil), de 17 configuradas |
| Candidatas descobertas | 11 |
| Validadas | 8 |
| Descartadas | 22 |
| `URGENTE` | 0 |
| `ALTA_PRIORIDADE` | 0 |
| `REVISAO` | 8 |

Nenhuma oportunidade atingiu `URGENTE` (que exige prazo em até 7 dias) nem `ALTA_PRIORIDADE` (que exige score ≥ 75 e confiança ≥ 0,70); as 8 validadas caíram em `REVISAO`. As duas chamadas do Ibermúsicas vencem em 11 dias e ficam fora do alerta `URGENTE` por pouco, merecendo tratamento manual de urgência mesmo sem acionar a regra. **Correção:** o VIDEOCLIPE-SE Festival foi retirado da lista de quase-urgentes nesta versão — seu regulamento traz dois prazos conflitantes (30/09/2026 no item 3.1 e 30/10/2026 no cronograma do item 8), sem indicação de qual prevalece, e não é correto inferir uma data para calcular dias até o prazo. A decisão foi ajustada de `Aplicar (condicional)` para `Monitorar` enquanto a organização não confirmar a data por escrito; o item continua em `REVISAO`. Apenas uma validada alcançou score ≥ 60 (Funarte Aberta, 63), e três das oito têm status `DESCONHECIDA` por bloqueio técnico de fonte.

## 2. Urgentes

Critério: `status_operacional` = `ABERTA` (inclui prorrogada confirmada) + decisão `APLICAR` ou `AVALIAR_COM_PARCERIA` + prazo em até 7 dias. Ordenado por prazo.

_Nenhum item urgente nesta rodada._

Observação: as duas chamadas do Ibermúsicas, com prazo em 11 dias, não acionam a regra `URGENTE`, mas devem receber tratamento manual de urgência.

| Título | Prazo | Decisão | Por que não é `URGENTE` |
|---|---|---|---|
| Ibermúsicas 2026 — Circulação de profissionais da música | 01/10/2026, 23:59 "horário do país do proponente" (fuso ambíguo) | Avaliar com parceria | Prazo em 11 dias, acima do limite de 7 dias |
| Ibermúsicas 2026 — Residências para artistas e pesquisadores | 01/10/2026, 23:59 "horário do país do proponente" (fuso ambíguo) | Avaliar com parceria | Prazo em 11 dias, acima do limite de 7 dias |

**Correção — VIDEOCLIPE-SE Festival — 4ª edição:** removido desta lista de quase-urgentes. O regulamento oficial traz dois prazos conflitantes e não resolvidos (item 3.1: 30/09/2026; cronograma do item 8: 30/10/2026), sem indicação de qual prevalece. Sem inferir a data correta, não é possível calcular dias até o prazo nem sustentar a decisão `Aplicar (condicional)` do relatório original, que dependia do prazo inferido (30/09). A decisão foi ajustada para `Monitorar` e o item permanece em `REVISAO` até confirmação oficial por escrito da organização. Ver seção 3b e seção 5.

## 2b. Prazo vencido em candidatura em preparação

Alerta crítico. Oportunidades em "Em preparação" ou "Pronto para inscrição" com edital encerrado ou prazo vencido.

_Nenhum caso nesta rodada._

## 3. Novas oportunidades prioritárias (score ≥ 60)

Ordenadas por score e, em seguida, por prazo. Marcar `ALTA_PRIORIDADE` quando score ≥ 75, `status_operacional` = `ABERTA` e confiança ≥ 0,70.

| Título | Instituição | País / território | Modalidade | Valor e moeda | Prazo (data, hora, fuso) | Score | Decisão | Prioridade | Confiança | Motivo de aderência | Maior risco | Próxima ação | Link oficial | Regulamento |
|---|---|---|---|---|---|---:|---|---|---:|---|---|---|---|---|
| Programa Funarte Aberta 2026 — Ocupação dos Espaços Culturais | Funarte/MinC | Brasil — nacional (editais nº 3/2026, Centro Técnico de Artes/RJ, e nº 5/2026, Complexo Funarte SP; há ainda MG, Centro de Teatro e Livraria Mário de Andrade, com páginas próprias não abertas) | Cessão gratuita de espaço para apresentação, ensaio, gravação, formação, intercâmbio e registro audiovisual | Sem repasse financeiro — o benefício é o espaço gratuito e a bilheteria integral ao proponente (ingresso até R$ 100, meia-entrada obrigatória). Moeda: BRL | Fluxo contínuo desde 30/03/2026 até 30/04/2027, 17h59 (horário de Brasília), "ou enquanto houver disponibilidade de pauta" | 63 | Aplicar | `REVISAO` | 0,70 | Aberta, inscrição gratuita, rota de elegibilidade confirmada por pessoa física e escopo que casa com show + live session gravada + registro audiovisual no mesmo bloco de pauta | A pauta pode esgotar muito antes de abril/2027, e os custos operacionais a cargo do proponente não foram localizados — espaço gratuito não significa evento barato | Extrair os PDFs dos editais 3/2026 e 5/2026 e consultar disponibilidade de pauta no CTA-RJ e no Complexo Funarte SP para o 1º semestre de 2027 | https://www.gov.br/funarte/pt-br/editais-1/editais-abertos/programa-funarte-aberta | https://www.gov.br/funarte/pt-br/editais/2026/programa-funarte-aberta/programa-funarte-aberta-2026-2013-ocupacao-dos-espacos-culturais-da-funarte-centro-tecnico-de-artes/regulamento-funarte-aberta-cta.pdf |

## 3b. Demais oportunidades validadas (score < 60)

Registradas para rastreabilidade. Ordenadas por score decrescente. Todas em `REVISAO`.

| Título | Instituição | País / território | Modalidade | Valor e moeda | Prazo (data, hora, fuso) | Score | Decisão | Confiança | Motivo de aderência | Maior risco | Próxima ação | Link oficial | Regulamento |
|---|---|---|---|---|---|---:|---|---:|---|---|---|---|---|
| VIDEOCLIPE-SE Festival — 4ª edição | Limonada Audiovisual, com Maria Bonita Filmes | Brasil — MG/BH; Mostra Competitiva nacional (20 selecionados) e Chamada de Produção restrita a BH e região metropolitana | Mostra competitiva de videoclipe | R$ 500,00 por prêmio, em quatro categorias. Inscrição gratuita. Moeda: BRL | **Conflito de fonte no regulamento oficial — nenhuma data inferida como correta:** item 3.1 indica 30/09/2026; cronograma do item 8 indica 30/10/2026. Hora e fuso não localizados em nenhuma das duas. Prazo real **não confirmado**, pendente de esclarecimento oficial por escrito | 54 | **Monitorar** (correção — ver nota abaixo) | 0,66 | Regulamento lido; aberta a PF maior de 18 anos ou PJ de qualquer estado; inscrição gratuita; a obra já precisa existir, não há produção a financiar | O conflito de datas dentro do próprio regulamento, que impede confirmar viabilidade de prazo; e a contrapartida do item 6.1.II, que autoriza exibição e reprodução no site do festival "sem limite de tempo ou de número de exibições". Condicionante adicional: depende de a Dhara ter videoclipe produzido no Brasil e lançado a partir de 2020 — dado não fornecido | Confirmar se existe videoclipe elegível; escrever à organização pedindo confirmação oficial por escrito de qual data prevalece (30/09 ou 30/10) e do horário-limite. Não inscrever com base em nenhuma das duas datas até a confirmação. Manter em `REVISAO` | https://www.videoclipesefestival.com.br/ | https://www.videoclipesefestival.com.br/regulamento/ |
| Ibermúsicas 2026 — Ayuda a la circulación de profesionales de la música | Programa Ibermúsicas | Multipaís ibero-americano — internacional | Mobilidade/circulação internacional — apoio exclusivamente para compra de passagens. Execução em 2027; resultados em 27/11/2026 | Não localizado. Moeda não localizada. (O número "até USD 10.000" circula em fonte terciária, **não tem lastro oficial e não deve ser usado**) | 01/10/2026, 23:59 "no horário do país do proponente" — ambíguo para o Brasil, que tem múltiplos fusos | 53 | Avaliar com parceria | 0,58 | Mobilidade internacional em programa do qual o Brasil é país membro; elegibilidade como pessoa física altamente provável | Sem destino e contraparte definidos no exterior não há objeto de inscrição; e o apoio cobre apenas passagem | Ler o PDF do regulamento e responder se há atividade ou convite confirmado em país membro para 2027 | https://www.ibermusicas.org/index.php/convocatorias/ | https://www.ibermusicas.org/wp-content/uploads/2026/05/1-Ayuda-a-la-circulacion-de-profesionales-de-la-musica-2026.pdf |
| Ibermúsicas 2026 — Ayuda a artistas e investigadores para residencias | Programa Ibermúsicas | Multipaís ibero-americano — internacional; destino livre, em qualquer parte do mundo | Residência artística/de pesquisa, duração mínima de 3 semanas, junto a instituição anfitriã. Execução em 2027 | Não localizado. Moeda não localizada | 01/10/2026, 23:59 horário do país do proponente (mesma ambiguidade de fuso) | 41 | Avaliar com parceria | 0,52 | Residência é formato prioritário e o destino é livre | Não foi confirmado se a carta da instituição anfitriã é exigida já na inscrição — se for, o prazo operacional real é de poucos dias úteis | Ler o PDF para responder se a carta de anfitriã é exigida na inscrição | https://www.ibermusicas.org/index.php/convocatorias/ | https://www.ibermusicas.org/wp-content/uploads/2026/06/3-Ayuda-a-artistas-e-investigadores-para-residencias-2026-ok.pdf |
| Résidences Institut français x Cité internationale des arts 2027–2028 | Institut français + Cité internationale des arts | França (Paris) — internacional | Residência de 3, 6 ou 9 meses em Paris, entre abril/2027 e abril/2028. Música é disciplina elegível | Bolsa de no mínimo €1.100/mês paga pelo parceiro associado, não pelo Institut français, que fornece apenas o ateliê-moradia. Moeda: EUR | 08/10/2026, 23h59 CET (Europe/Paris) | 35 | Avaliar com parceria | 0,84 | Alta aderência artística e a Dhara cumpre o critério mais duro, de residir fora da França há 5+ anos | Restrição confirmada em fonte oficial — "Applications submitted directly by artists will be deemed ineligible". Só um parceiro cultural associado pode submeter, e ele assume bolsa, passagens, seguro e visto. A IFA Sounds só entraria como pagadora, não como beneficiária: não é rota de captação | Pedir à Cité/Institut français a lista de parceiros habilitados no Brasil e o calendário da edição 2028–2029; tratar como pauta de relacionamento, não de inscrição em 2026 | https://www.institutfrancais.com/fr/programme/residence-mobilite-professionnelle/residences-institut-francais-x-cite-internationale | Inscrição: https://ifprog.emundus.fr/fr/campagne-info?view=programme&cid=343 |
| Edital Ambev Brasilidades 2026 | Cervejaria Ambev | Brasil — nacional | Patrocínio via leis estaduais de incentivo (renúncia fiscal) | Valor por projeto não localizado. O teto de R$ 67 milhões é do programa inteiro (cultura + esporte). Moeda: BRL | Não localizado. A página oficial renderiza o placeholder `{{oportunidade.encerramento_das_inscricoes}}` em vez de uma data. O prazo de 30/09/2026 vem só de agregadores e não foi aceito | 17 | Monitorar | 0,32 | Música é área elegível e PJ com e sem fins lucrativos é aceita, mas há barreira estrutural | Exige projeto já aprovado (excepcionalmente, apenas inscrito) em lei estadual de incentivo à cultura. Sem isso a IFA não concorre, independentemente do prazo | Responder se a IFA ou a Dhara têm projeto aprovado ou inscrito em lei estadual de incentivo | https://editalbrasilidades.com.br (redireciona para a plataforma oficial de inscrição) | Inscrição: https://prosas.com.br/editais/16452-edital-ambev-brasilidades-2026 |
| Tallinn Music Week 2027 — Artist Applications | Tallinn Music Week | Estônia (Tallinn) — internacional | Showcase de festival (evento em abril/2027) | Não localizado. Taxa de inscrição: não localizada | Não localizado. `tmw.ee` retornou HTTP 429 em todas as tentativas, na descoberta e na validação; o site da produtora recusou conexão. Agregadores divergem entre 26 e 27/10/2026, sem valor probatório | 8 | Monitorar | 0,12 | Showcase relevante, mas nenhum campo pôde ser confirmado | Perder a janela por bloqueio técnico persistente; e nada indica que passagem aérea seja coberta | Recoletar `tmw.ee` em 3 e em 7 dias. Não alocar tempo da Dhara até haver fonte oficial legível | https://tmw.ee/artist-applications (inacessível) | Não localizado |
| Edital de Seleção Pública de Patrocínios 2026 | Embratur | Brasil — nacional | Patrocínio institucional | Não localizado | Não localizado. O site oficial retornou HTTP 403 e o PDF do edital não retornou texto extraível. O prazo aparente de 03/10/2026 existe apenas em buscadores e agregadores | 0 | Monitorar | 0,15 | Nenhum dado foi confirmado. **O score 0 é piso após penalidades e significa "sem base para avaliar", não "avaliado e reprovado"** | O edital é de promoção turística internacional e pode excluir projeto de música autoral isolado — hipótese, não achado; somada à janela curta | Acionar verificação humana urgente em até 48h, via Diário Oficial da União e canal institucional da Embratur | https://patrocinio.embratur.com.br/ (HTTP 403) | https://patrocinio.embratur.com.br/wp-content/uploads/2026/01/Edital-de-Selecao-Publica-de-Patrocinios-2026-1.pdf |

**Nota de correção — VIDEOCLIPE-SE Festival — 4ª edição:** o relatório original (`2026-09-20-diario.md`) tratava 30/09/2026 como "prazo operacional" e classificava a decisão como `Aplicar (condicional)`, com a próxima ação "Inscrever até 29/09" — tudo isso derivado de uma inferência sobre qual das duas datas do regulamento prevalecia. Nesta correção: (1) as duas datas do regulamento (30/09 no item 3.1 e 30/10 no cronograma do item 8) são registradas como conflito de fonte, sem inferir qual é a correta; (2) o item permanece em `REVISAO`, agora explicitamente até confirmação oficial por escrito da organização sobre qual data prevalece; (3) a decisão foi ajustada de `Aplicar (condicional)` para `Monitorar`, porque dependia do prazo inferido — sem saber qual data vale, não é possível afirmar que o prazo é viável, condição exigida para `Aplicar`. Score (54) e confiança (0,66) não foram recalculados nesta correção: a alteração é de tratamento do prazo e da decisão, não uma nova rodada de scoring pelo `dhara-fit-scorer`.

Status validado e operacional: **Aberta** para Funarte Aberta, VIDEOCLIPE-SE (inscrições abertas; prazo final **não confirmado** — conflito de fonte entre 30/09 e 30/10, ver nota de correção acima), as duas chamadas do Ibermúsicas e a residência Institut français x Cité; **Desconhecida** para Ambev Brasilidades, Tallinn Music Week e Embratur. Fonte oficial não confirmada em Tallinn Music Week e Embratur; parcial no Ambev Brasilidades.

## 4. Atualizações

Mudanças de prazo, status, regulamento, valor ou elegibilidade em oportunidades já conhecidas.

_Nenhuma atualização de fonte nesta rodada._ Primeira rodada: `data/reports/` estava vazio, as 8 validadas são novas e não há encerramentos a registrar. Nenhuma duplicata — as duas linhas do Ibermúsicas são chamadas distintas da mesma convocatória. Esta própria versão do relatório é uma correção editorial do tratamento do prazo/decisão do VIDEOCLIPE-SE, não uma atualização de fonte — ver nota de correção no topo do documento.

## 5. Revisão humana necessária

As 8 oportunidades validadas exigem revisão humana. As três primeiras linhas são perguntas eliminatórias: cada uma bloqueia uma decisão inteira.

| Oportunidade | Ponto de decisão ou informação faltante | Motivo (`REVISAO`) | Fonte |
|---|---|---|---|
| VIDEOCLIPE-SE Festival — 4ª edição | **Pergunta eliminatória:** a Dhara tem videoclipe produzido no Brasil e lançado a partir de 2020? Sem isso não há objeto de inscrição | Campo crítico ausente (elegibilidade da obra) | https://www.videoclipesefestival.com.br/regulamento/ |
| Edital Ambev Brasilidades 2026 | **Pergunta eliminatória:** a IFA Sounds ou a Dhara têm projeto já aprovado — ou ao menos inscrito — em lei estadual de incentivo à cultura? | Elegibilidade de PJ; campo crítico ausente | https://editalbrasilidades.com.br |
| Ibermúsicas 2026 — Circulação de profissionais da música | **Pergunta eliminatória:** há atividade, convite ou contraparte confirmada em país membro do Ibermúsicas para 2027? | Necessidade de parceiro/anfitrião no exterior | https://www.ibermusicas.org/index.php/convocatorias/ |
| VIDEOCLIPE-SE Festival — 4ª edição | Conflito de datas dentro do regulamento oficial: item 3.1 diz 30/09/2026, cronograma do item 8 diz 30/10/2026. Hora e fuso não localizados em nenhuma das duas. Nenhuma data foi inferida como correta; a organização precisa confirmar por escrito. **Decisão ajustada nesta correção de `Aplicar (condicional)` para `Monitorar`**, pois dependia do prazo inferido (30/09) | Conflito entre seções do regulamento; prazo e horário ambíguos; item mantido em `REVISAO` até confirmação oficial | https://www.videoclipesefestival.com.br/regulamento/ |
| VIDEOCLIPE-SE Festival — 4ª edição | Decisão sobre a contrapartida do item 6.1.II, que autoriza exibição e reprodução no site do festival "sem limite de tempo ou de número de exibições" — e se há contrato de distribuição ou exclusividade sobre o videoclipe | Requisito contratual de cessão; documentação | https://www.videoclipesefestival.com.br/regulamento/ |
| Ibermúsicas 2026 — Circulação / Residências | Valor e moeda não localizados; fuso ambíguo ("23:59 no horário do país do proponente", e o Brasil tem múltiplos fusos). O número "até USD 10.000" é de fonte terciária sem lastro oficial | Campo crítico ausente; fuso ambíguo; conflito de fonte | https://www.ibermusicas.org/index.php/convocatorias/ |
| Ibermúsicas 2026 — Residências para artistas e pesquisadores | Não foi confirmado se a carta da instituição anfitriã é exigida já na inscrição. Se for, o prazo operacional real é de poucos dias úteis | Necessidade de anfitrião/carta-convite; campo ausente | https://www.ibermusicas.org/wp-content/uploads/2026/06/3-Ayuda-a-artistas-e-investigadores-para-residencias-2026-ok.pdf |
| Résidences Institut français x Cité internationale des arts 2027–2028 | Candidatura direta de artista é inelegível por regra oficial. Decidir se vale abrir relacionamento com parceiro habilitado no Brasil para a edição 2028–2029, sabendo que a IFA Sounds entraria como pagadora (bolsa, passagens, seguro, visto), não como beneficiária | Necessidade de parceiro/coprodutor; cofinanciamento; visto | https://www.institutfrancais.com/fr/programme/residence-mobilite-professionnelle/residences-institut-francais-x-cite-internationale |
| Programa Funarte Aberta 2026 | Custos operacionais a cargo do proponente não localizados; disponibilidade de pauta no CTA-RJ e no Complexo Funarte SP não consultada; páginas de MG, Centro de Teatro e Livraria Mário de Andrade não abertas | Campo crítico ausente | https://www.gov.br/funarte/pt-br/editais-1/editais-abertos/programa-funarte-aberta |
| Edital Ambev Brasilidades 2026 | Prazo não localizado — a página oficial renderiza um placeholder no lugar da data; agregadores indicam 30/09/2026, não aceito | Campo crítico ausente; conflito entre página oficial e agregadores | https://editalbrasilidades.com.br |
| Tallinn Music Week 2027 — Artist Applications | Nenhum campo confirmado: prazo, valor e taxa de inscrição não localizados. Agregadores divergem entre 26 e 27/10/2026 | Fonte oficial inacessível (HTTP 429); conflito entre agregadores | https://tmw.ee/artist-applications |
| Edital de Seleção Pública de Patrocínios 2026 (Embratur) | Nenhum campo confirmado. Score 0 é piso após penalidades e significa "sem base para avaliar", não reprovação. Prazo aparente de 03/10/2026 só em buscadores | Fonte oficial inacessível (HTTP 403); PDF sem texto extraível; campo crítico ausente | https://patrocinio.embratur.com.br/ |
| Todas as oportunidades com rota de PJ | CNAE, sede, tempo de CNPJ e certidões da IFA Sounds não foram fornecidos e não podem ser presumidos | Dúvida de elegibilidade de PJ, CNPJ, sede e certidões | — |
| Oportunidades internacionais (Ibermúsicas, Institut français x Cité, Tallinn Music Week) | Nível de francês e de inglês da Dhara; disponibilidade de agenda para 3 semanas ou para 3–9 meses fora do Brasil em 2027 | Idioma; mobilidade; visto | — |

## 6. Próximas ações

1. Responder as três perguntas eliminatórias (videoclipe elegível; projeto em lei estadual de incentivo; contraparte confirmada em país membro do Ibermúsicas) — custam minutos e destravam três decisões.
2. Escrever hoje à organização do VIDEOCLIPE-SE pedindo, por escrito, a data correta e o horário-limite, dado o conflito entre os itens 3.1 e 8 do regulamento. Manter a decisão em `Monitorar` e o item em `REVISAO` até a confirmação oficial; não inscrever com base em nenhuma das duas datas até então.
3. Extrair os PDFs dos regulamentos do Ibermúsicas e da Funarte, que hoje bloqueiam valor, elegibilidade de PJ e exigência de carta de anfitriã.
4. Acionar verificação humana urgente da Embratur em até 48h, via Diário Oficial da União e canal institucional.
5. Consultar disponibilidade de pauta no Complexo Funarte SP e no Centro Técnico de Artes/RJ para o 1º semestre de 2027.

## 7. Limitações da rodada

- **Fontes inacessíveis:** `tmw.ee` (HTTP 429, nas duas etapas); `patrocinio.embratur.com.br` (HTTP 403); PDF do edital Embratur (sem texto extraível); `culteditais.cultura.gov.br` / plataforma CultBR do MinC (HTTP 403 — bloco inteiro de chamadas federais PNAB não verificado); `shiftworks.ee` (conexão recusada); `brasilidades.com.br` (erro de certificado TLS); `som.vc` (exige autenticação); listagens em JavaScript não extraíveis na PROSAS, no Fomento CultSP e no Portal do Fomento de SP.
- **Limitação técnica crítica do ambiente:** nenhum PDF pôde ser lido nesta rodada (`pdftoppm` ausente, Bash indisponível para os subagentes). Isso impediu extrair valor, moeda, elegibilidade e documentos dos regulamentos do Ibermúsicas, da Funarte e da Embratur. É limitação estrutural a corrigir antes da próxima rodada.
- **Prazos não confirmados:** Ambev Brasilidades, Tallinn Music Week e Embratur. Conflito interno de datas no regulamento do VIDEOCLIPE-SE (item 3.1: 30/09/2026; item 8: 30/10/2026), sem inferência de qual prevalece — nesta correção, a decisão do VIDEOCLIPE-SE foi ajustada de `Aplicar (condicional)` para `Monitorar` em consequência, e o item permanece em `REVISAO` até confirmação oficial por escrito. Fuso ambíguo nas duas chamadas do Ibermúsicas.
- **Cobertura parcial:** 5 das 17 fontes não foram consultadas — `diarios_oficiais`, `sesc`, `centros_culturais`, `redes_musica_independente` e `mulheres_na_musica` (esta última é prioridade temática declarada e não recebeu nenhuma consulta). 21 UFs e quase todas as capitais ficaram sem varredura; Norte e Centro-Oeste sem nenhuma consulta. Consultas por idioma: português 13, inglês 4, francês 1, espanhol 1, alemão 0. Não houve consulta por categoria sobre artes integradas, acessibilidade, cultura digital, economia criativa e formação de público. A descoberta encerrou com 11 candidatas (limite de 12 não atingido) por limite de turnos do subagente, não por esgotamento das fontes.
- **Candidatas descobertas e não validadas (3), por decisão de escopo da rodada piloto (limite de 8):** SXSW 2027 Music Festival Showcase (prazo aparente 20/11/2026); CreativeSP 2026 missão WOMEX (janela provavelmente encerrada); MinC Circulação e Participação Audiovisual no Exterior (prazo aparente 06/11/2026, praticamente todos os campos não localizados). Ficam para a próxima rodada.
- **Erros de coleta corrigidos na validação:** a URL do VIDEOCLIPE-SE apurada na descoberta não resolve DNS (o domínio correto é `videoclipesefestival.com.br`); o domínio oficial do Brasilidades é `editalbrasilidades.com.br`; e um agregador divulgou como prazo de inscrição do Instituto Cultural Vale o que era, na verdade, data de divulgação do resultado.
- **Sincronização com o Notion:** não aplicável — não configurada.

## 8. Propostas de atualização de fontes

URLs sugeridas para fontes com `url: null` em `config/sources.yaml` — as 17 fontes configuradas estão com `url: null`. **Não validadas.** O arquivo de configuração não foi alterado e não deve ser alterado automaticamente.

| Fonte (`id`) | Nome | URL sugerida | Onde foi encontrada | Evidência de que é oficial | Situação |
|---|---|---|---|---|---|
| `prosas` | PROSAS | https://prosas.com.br/editais (301 para produtos.prosas.com.br/editais) | Busca `site:prosas.com.br`; redirecionamento observado | Hospeda as páginas de inscrição apontadas oficialmente pela Funarte | Proposta — requer validação humana |
| `minc` | Ministério da Cultura e vinculadas | https://www.gov.br/funarte/pt-br/editais-1/editais-abertos e https://culteditais.cultura.gov.br/ | Página gov.br acessada; CultBR citado em edital PNAB | Domínio gov.br é o portal oficial federal. **CultBR retornou HTTP 403** | Proposta — requer validação humana |
| `secretarias_estaduais` | Secretarias estaduais de cultura | https://www.cultura.sp.gov.br/ (SP), https://www.bahiapnab.com.br/editais (BA), https://www.cultura.pe.gov.br/ (PE) | Busca por nome do órgão | Domínios .sp.gov.br e .pe.gov.br são governamentais. **bahiapnab.com.br é .com.br, não .gov.br — requer checagem extra** | Proposta — requer validação humana |
| `secretarias_municipais_capitais` | Secretarias municipais das capitais | https://prefeitura.sp.gov.br/web/cultura/editais, https://prefeitura.poa.br/smc/editais | Resultados de busca | Domínios de prefeitura municipal | Proposta — requer validação humana |
| `sesi` | SESI e equivalentes | https://www.sesisp.org.br/cultura/editais | Busca por edital SESI-SP música | Domínio institucional do SESI-SP, com seção própria de editais | Proposta — requer validação humana |
| `festivais_showcases_brasil` | Festivais e showcases no Brasil | https://www.videoclipesefestival.com.br/ | Corrigido na validação | Site próprio do festival; regulamento oficial lido nesta rodada | Proposta — requer validação humana |
| `mobilidade_artistica` | Mobilidade e intercâmbio | https://www.ibermusicas.org/index.php/convocatorias/ e https://on-the-move.org/news/deadlines | Funarte/gov.br linka Ibermúsicas | Ibermúsicas é referenciado por página oficial da Funarte. **On the Move não é órgão público — classificar como parceiro** | Proposta — requer validação humana |
| `residencias_internacionais` | Residências internacionais | https://www.citeinternationaledesarts.fr/en/appels-a-candidature/ e https://www.institutfrancais.com/ | Busca em francês | Instituições francesas com sites institucionais e formulário oficial | Proposta — requer validação humana |
| `festivais_showcases_internacionais` | Festivais e mercados internacionais | https://sxsw.com/apply/showcase-applications/ e https://tmw.ee/artist-applications | Buscas em inglês | Domínios próprios dos festivais. **tmw.ee retornou HTTP 429** | Proposta — requer validação humana |
| `instituicoes_culturais_estrangeiras` | Instituições culturais estrangeiras | https://www.institutfrancais.com/fr/programme/residence-mobilite-professionnelle/residences-institut-francais-x-cite-internationale | Link oficial na página da Cité | Institut français é a agência oficial de ação cultural exterior da França | Proposta — requer validação humana |
| `fundacoes_institutos` | Fundações e institutos culturais | https://institutoculturalvale.org/ e https://patrocinio.embratur.com.br/ | Buscas por patrocínio cultural 2026 | Sites institucionais. **Embratur retornou HTTP 403** | Proposta — requer validação humana |

## 9. Sincronização com o Notion

- **Situação:** não configurada
- **Operações preparadas:** 0 oportunidades e 0 páginas de relatório. `config/notion.yaml` tem `sincronizacao.habilitada: false`, todos os `database_id` e `data_source_id` em `null` e `schema_verificado: false`
- **Por nível:** não aplicável
- **Payload:** não gerado — a usuária pediu explicitamente que nenhum payload fosse preparado nesta rodada
- **Log de sincronização:** não aplicável
- **Pendências de rodadas anteriores:** nenhuma (primeira rodada)

## Decisões humanas necessárias

- **Perguntas eliminatórias** (cada resposta destrava ou encerra uma decisão inteira):
  1. A Dhara tem videoclipe produzido no Brasil e lançado a partir de 2020? Decide a inscrição no VIDEOCLIPE-SE — cujo prazo **não está confirmado**: o regulamento traz duas datas conflitantes (30/09/2026 no item 3.1 e 30/10/2026 no cronograma do item 8), sem indicação de qual prevalece. A organização precisa confirmar por escrito antes de qualquer decisão de inscrição.
  2. A IFA Sounds ou a Dhara têm projeto já aprovado — ou ao menos inscrito — em lei estadual de incentivo à cultura? Decide o Edital Ambev Brasilidades 2026.
  3. Há atividade, convite ou contraparte confirmada em país membro do Ibermúsicas para 2027? Decide a chamada de circulação do Ibermúsicas, com prazo em 01/10/2026.
- **Correção do VIDEOCLIPE-SE (prazo e decisão):** o item permanece em `REVISAO`; a decisão foi ajustada nesta versão de `Aplicar (condicional)` para `Monitorar`, porque dependia do prazo inferido (30/09/2026). O prazo real não está confirmado — a organização precisa esclarecer por escrito qual das duas datas do regulamento (30/09 no item 3.1 ou 30/10 no cronograma do item 8) prevalece.
- **Pendências documentais da IFA Sounds:** informar CNAE, sede, tempo de CNPJ e situação das certidões. Não foram fornecidos e não podem ser presumidos.
- **Cessão de exibição no VIDEOCLIPE-SE:** decidir se aceita a contrapartida do item 6.1.II do regulamento, que autoriza exibição e reprodução da obra no site do festival "sem limite de tempo ou de número de exibições" — verificando antes se há contrato de distribuição ou exclusividade sobre o videoclipe.
- **Disponibilidade e idiomas da Dhara:** confirmar nível de francês e de inglês e disponibilidade de agenda para 3 semanas (Ibermúsicas residências) ou 3–9 meses (Institut français x Cité) fora do Brasil em 2027.
- **Residência Institut français x Cité:** decidir se vale abrir relacionamento com parceiro cultural habilitado no Brasil visando a edição 2028–2029, sabendo que a candidatura direta de artista é inelegível e que a IFA Sounds entraria como pagadora de bolsa, passagens, seguro e visto, não como beneficiária.
