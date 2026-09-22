# Orquestração da rodada

Este documento descreve como a **sessão principal do Claude Code** coordena uma rodada do Radar de Editais da Dhara / IFA Records.

A orquestração não é um subagente. No Claude Code, subagentes não podem criar outros subagentes; por isso quem delega é a própria sessão principal, guiada por `CLAUDE.md` e por este documento. Este arquivo substitui o antigo `.claude/agents/edital-orchestrator.md`.

## Papéis

| Papel | Quem executa | Arquivo de instrução |
|---|---|---|
| Orquestração, consolidação e sincronização com o Notion | Sessão principal do Claude Code | `CLAUDE.md`, este documento e `docs/07_NOTION_OPERACAO.md` |
| Descoberta | Subagente `opportunity-discovery` | `.claude/agents/opportunity-discovery.md` |
| Validação | Subagente `edital-validator` | `.claude/agents/edital-validator.md` |
| Elegibilidade e score | Subagente `dhara-fit-scorer` | `.claude/agents/dhara-fit-scorer.md` |
| Relatórios, alertas e payloads do Notion | Subagente `edital-reporter` | `.claude/agents/edital-reporter.md` |

Nenhum subagente acessa o Notion. A sessão principal é a única responsável pela sincronização.

## Contexto fixo

- Artista: Dhara Guimarães, cantora e compositora independente brasileira.
- Projeto prioritário: álbum autoral “Nada disso é só meu”, que combina linguagem acústica/intimista e uma face orientada por beats; temas de relações, memória, cidade, intimidade, narrativas coletivas e cultura brasileira contemporânea.
- Proponente/representante possível: IFA Sounds, nome comercial IFA Records.
- A IFA Sounds é pessoa jurídica brasileira com CNPJ, enquadrada no Simples Nacional.
- Nunca tratar a IFA Sounds como MEI e nunca presumir regras, tetos, CNAE, tempo de constituição, certidões ou dados fiscais não comprovados.
- Cobertura: Brasil inteiro e oportunidades internacionais. Nunca limitar a busca a São Paulo.
- Uma exigência de sede, residência, CNPJ local, entidade anfitriã ou parceiro territorial não gera descarte automático. Avaliar se existe rota realista de parceria, coprodução, convite, contratação artística, circulação ou instituição anfitriã.

## Pré-condições

Antes de qualquer rodada, a sessão principal deve ler:

- `CLAUDE.md`
- `docs/01_CONTEXTO_DHARA_IFA.md`
- `docs/02_CRITERIOS_DE_ELEGIBILIDADE.md`
- `docs/03_FONTES_DE_MONITORAMENTO.md`
- `docs/04_PIPELINE_E_STATUS.md`
- `docs/05_KIT_DOCUMENTAL.md`
- `docs/06_ORQUESTRACAO_DA_RODADA.md`
- `docs/07_NOTION_OPERACAO.md`
- `config/sources.yaml`
- `config/scoring.yaml`
- `config/notion.yaml`
- O relatório mais recente em `data/reports/`, se houver.

E confirmar que estes subagentes estão disponíveis (por exemplo, com `/agents`):

- `opportunity-discovery`
- `edital-validator`
- `dhara-fit-scorer`
- `edital-reporter`

Se algum arquivo obrigatório ou subagente estiver ausente, ilegível ou não puder ser invocado no ambiente atual, não fingir delegação. Informar:

1. O item ausente ou indisponível.
2. O caminho ou nome esperado.
3. O impacto no fluxo.
4. A correção necessária.

## Preparação

Antes da etapa 1, a sessão principal define o escopo temporal e geográfico pedido pela pessoa usuária. Sem instrução, usar Brasil e exterior, oportunidades abertas e anúncios recentes, com prazo nos próximos 90 dias.

Na Preparação, a sessão principal também verifica, sem gravar nada, se o Notion está acessível e se `config/notion.yaml` está completo. O resultado (acessível, inacessível ou não configurado) é repassado ao `edital-reporter` e decide se a etapa 7 acontece.

## Sequência obrigatória

1. **Descoberta — `opportunity-discovery`.** Repassar o escopo. O subagente usa as fontes de `config/sources.yaml` e também procura URLs oficiais para as fontes com `url: null` (ver "Fontes sem URL configurada").
2. **Validação — `edital-validator`.** Delegar cada candidata relevante, repassando a linha completa da descoberta (URLs e evidência). O validador atribui `status_validado` e `status_operacional`, conforme `docs/04_PIPELINE_E_STATUS.md`.
3. **Normalização e deduplicação — sessão principal.**
   - Unificar registros que apontem para a mesma chamada (mesma URL oficial, mesmo identificador ou mesmo título e instituição).
   - Manter a fonte de maior autoridade como referência e preservar as demais URLs como `url_descoberta`.
   - Comparar com o relatório anterior e com `data/validated/` para marcar itens novos, atualizados (inclusive prorrogações) ou encerrados.
   - Não alterar nenhum dado validado; apenas unir e marcar.
4. **Score — `dhara-fit-scorer`.** Enviar somente os registros validados e deduplicados.
5. **Relatório — `edital-reporter`.** Enviar:
   - As saídas do `edital-validator` e do `dhara-fit-scorer`.
   - As métricas da rodada vindas do `opportunity-discovery`: consultas por idioma, fontes consultadas, número de candidatas, itens descartados e lacunas.
   - As propostas de URL para fontes com `url: null`.
   - A lista de itens novos, atualizados e encerrados da etapa 3.
   - O resultado da verificação de acesso ao Notion feita na Preparação.

   O reporter grava o relatório local e, se a sincronização estiver habilitada, prepara os payloads em `data/reports/AAAA-MM-DD-notion-payload.json`.
6. **Consolidação — sessão principal.** Consolidar as saídas sem alterar dados, score, evidências ou conclusões dos subagentes.
7. **Sincronização com o Notion — sessão principal.** Somente se `config/notion.yaml` tiver `sincronizacao.habilitada: true`, IDs resolvidos e `schema_verificado: true`. Seguir `docs/07_NOTION_OPERACAO.md`:
   - ler o schema das duas databases com `notion-fetch` e comparar com `docs/07`;
   - selecionar somente oportunidades com decisão `APLICAR`, `AVALIAR_COM_PARCERIA` ou `MONITORAR`;
   - consultar a chave de deduplicação de cada uma;
   - classificar cada operação como factual, estratégica ou bloqueada, conforme `config/notion.yaml` (`politica_atualizacao`), inclusive a regra de prazo vencido em candidatura em preparação;
   - apresentar o resumo das operações factuais em lote e cada proposta estratégica com a prévia completa de `docs/07`;
   - gravar as factuais e somente as estratégicas aprovadas, e ler de volta para conferir;
   - por último, criar a página do relatório na database `Relatórios do Radar — IFA Records`, com o resultado da sincronização e a relação para as oportunidades;
   - registrar tudo em `data/reports/AAAA-MM-DD-sync-notion.md`.

   Se o Notion estiver inacessível ou a verificação falhar, pular esta etapa, registrar a falha no log de sincronização e informar na consolidação. A rodada não é interrompida.

   Em execução agendada (rotina na nuvem, sem pessoa usuária presente), vale a seção "Modo agendado" de `docs/07_NOTION_OPERACAO.md`, no lugar da apresentação prévia e da aprovação por escrita descritas acima.

## Modo econômico (rodada agendada)

Ajustes para reduzir o consumo em rodadas agendadas, sem perder qualidade. Valem quando a rodada é executada por rotina agendada; onde indicado, também melhoram rodadas interativas.

### Execução dos subagentes

- Os subagentes rodam em primeiro plano, um de cada vez. É proibido lançá-los em segundo plano e ficar consultando se terminaram: a sessão principal aguarda o retorno de cada subagente antes de chamar o próximo.

### Leitura mínima na preparação

- Na preparação de uma rodada agendada, a sessão principal lê apenas `docs/06_ORQUESTRACAO_DA_RODADA.md`, a seção "Modo agendado" de `docs/07_NOTION_OPERACAO.md` e `config/notion.yaml`. Os demais arquivos da lista de "Pré-condições" só são lidos quando uma etapa deles precisar.

### Triagem antes da validação

- Etapa nova, entre a descoberta (etapa 1) e a validação (etapa 2). A sessão principal lê o campo `triagem_sugerida` de cada candidata (ver `.claude/agents/opportunity-discovery.md`). As candidatas marcadas pela descoberta, com evidência, como claramente não abertas ou claramente inelegíveis vão direto para `MONITORAR` ou `DESCARTAR`, sem validação completa. Só as candidatas com `triagem_sugerida = validar` seguem para o `edital-validator`.

### Deduplicação antes da validação

- Antes de validar, a sessão principal consulta o pipeline do Notion pela chave de deduplicação das candidatas que passaram na triagem. Se a oportunidade já existe, foi validada há menos de 7 dias e não tem prazo final nos próximos 10 dias, não é revalidada nesta rodada: registrar como "mantida sem revalidação". As demais seguem para a validação.

### Formato de entrega entre agentes

- A entrega entre agentes é compacta: só os campos do contrato de saída de cada agente, sem prosa e sem repetir instruções. Evidências literais têm no máximo 25 palavras.

### Encerramento

- Ao final da rodada, encerrar. Não assinar, observar nem comentar pull requests.

## Fontes sem URL configurada

- Usar primeiro as fontes com URL configurada em `config/sources.yaml`.
- Para fontes com `url: null`, o `opportunity-discovery` busca a página oficial e registra uma **proposta** de URL com evidência (onde foi encontrada e por que parece oficial).
- As propostas entram no relatório, na seção "Propostas de atualização de fontes", marcadas como não validadas.
- Ninguém edita `config/sources.yaml` automaticamente. A inclusão de uma URL depende de validação e aprovação humana.
- Nunca inventar nem preencher uma URL sem validação.
- A PROSAS é a fonte prioritária de descoberta no Brasil, mas sua página não pode ser a única evidência de status, prazo, valor ou elegibilidade quando houver regulamento ou fonte organizadora disponível.

## Gravação local

- O `edital-reporter` pode gravar relatórios e payloads do Notion somente em `data/reports/`.
- A sessão principal grava o log de sincronização em `data/reports/AAAA-MM-DD-sync-notion.md` (arquivo novo, sem sobrescrever).
- A sessão principal só grava em `data/inbox/`, `data/validated/` e `data/archive/` quando a pessoa usuária pedir explicitamente para registrar histórico.
- Alterações em `CLAUDE.md`, `README.md`, `docs/`, `config/`, `templates/` e `.claude/` exigem plano prévio e aprovação humana. Isso inclui `config/sources.yaml`: propostas de URL vão para o relatório, não para o arquivo.

## Regras de qualidade

- Edital, regulamento, retificação e página oficial prevalecem sobre agregadores, mídia, redes sociais e newsletters.
- PROSAS é uma fonte importante de descoberta e monitoramento no Brasil. Usá-la no radar, mas validar prazo, status, elegibilidade e regulamento na fonte organizadora/oficial sempre que ela estiver disponível.
- Não chamar algo de “aberto” sem evidência atual: prazo futuro claro, status oficial, plataforma ativa ou comunicação institucional recente.
- Não inventar prazo, valor, elegibilidade, moeda, país elegível, documentação, contrapartida ou possibilidade de inscrição.
- Quando faltar informação essencial, usar `não localizado` e gerar prioridade `REVISAO`.
- Preservar URL, fonte, data/hora de verificação e evidência textual de cada afirmação crítica.
- Não confundir vagas de emprego, concursos públicos, cursos ou formações isoladas com editais para projetos artísticos.
- Usar somente os valores internos padronizados de `docs/04_PIPELINE_E_STATUS.md`: status do funil sem acento, decisões `APLICAR`, `AVALIAR_COM_PARCERIA`, `MONITORAR`, `DESCARTAR` e prioridades `URGENTE`, `ALTA_PRIORIDADE`, `REVISAO`. Nos relatórios, exibir os rótulos legíveis.
- Tratar uma chamada `PRORROGADA` como aberta somente pelo campo `status_operacional`, preservando o `status_validado` original.

## Limites de ação

A sessão principal e os subagentes nunca devem:

- Submeter inscrições.
- Enviar e-mails, mensagens ou documentos.
- Assinar declarações, contratos ou formulários.
- Fazer pagamentos, compras, contratações ou compromissos.
- Gravar no Notion fora da etapa 7 ou sem a confirmação prevista em `docs/07_NOTION_OPERACAO.md`.
- Apagar, arquivar ou enviar para a lixeira qualquer página ou database do Notion, ou alterar seu schema durante a operação.
- Dar a um subagente acesso a ferramentas do Notion.
- Tentar burlar login, CAPTCHA, paywall, robots.txt, termos de uso, anti-bot ou limites de acesso.

## Modo de agente único

Se os subagentes não estiverem disponíveis, a rodada só pode seguir em `modo_agente_unico` com autorização expressa da pessoa usuária. Nesse caso, manter a mesma sequência lógica e identificar a saída como `modo_agente_unico`.

## Contrato de saída da consolidação

Retornar em português do Brasil:

1. Resumo da execução e escopo usado.
2. Modo de execução: `subagentes_formais` ou `modo_agente_unico`.
3. Fontes consultadas, sucessos, limitações e falhas.
4. Oportunidades novas, atualizadas, encerradas e descartadas.
5. Ranking de oportunidades por decisão, score e proximidade de prazo.
6. Alertas `URGENTE`, `ALTA_PRIORIDADE` e `REVISAO`.
7. Pendências documentais, territoriais, jurídicas e de parceria.
8. Propostas de atualização de fontes (URLs sugeridas, não validadas).
9. Resultado da sincronização com o Notion: operações factuais gravadas, propostas estratégicas aprovadas, recusadas ou adiadas, operações bloqueadas e falhas.
10. Próximas ações humanas recomendadas, no máximo cinco.
11. Caminhos dos arquivos gravados em `data/reports/` (relatório, payload e log de sincronização).
