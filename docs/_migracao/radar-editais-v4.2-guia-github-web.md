# Aplicar a v4.2 pelo GitHub web — Radar de Editais Dhara / IFA Records

Este guia substitui a aplicação por terminal. Fonte de verdade: `radar-editais-v4.2-principal.patch`
(SHA-256 `6e99a0a54a93acf5480368ae12b6f54cb9ac0ba033aef6fabe945a7dc2da942e`).
O pacote `radar-editais-v4.2-arquivos.zip` traz os 20 arquivos na versão final, já com todas as mudanças do patch.

Nada foi aplicado no seu repositório. Todos os passos abaixo são executados por você, no navegador.

## Resumo das mudanças

- 12 arquivos criados
- 8 arquivos modificados
- 1 arquivo removido: `.claude/agents/edital-orchestrator.md`
- `.claude/settings.json` NÃO faz parte desta PR

### Criados (12)

| Caminho | O que é |
|---|---|
| `docs/06_ORQUESTRACAO_DA_RODADA.md` | Orquestração da rodada pela sessão principal (substitui o antigo agente orquestrador) |
| `docs/07_NOTION_OPERACAO.md` | Operação do Notion: databases, política de escrita, níveis de atualização, primeira conexão |
| `config/sources.yaml` | Fontes monitoradas |
| `config/scoring.yaml` | Pesos, penalidades e limiares do score |
| `config/notion.yaml` | IDs do Notion (nulos) e política de atualização |
| `templates/daily-report.md` | Modelo do relatório diário |
| `templates/weekly-report.md` | Modelo do relatório semanal |
| `templates/opportunity-record.md` | Modelo do registro de oportunidade |
| `data/inbox/.gitkeep` | Pasta de trabalho |
| `data/validated/.gitkeep` | Pasta de trabalho |
| `data/reports/.gitkeep` | Pasta de trabalho |
| `data/archive/.gitkeep` | Pasta de trabalho |

### Modificados (8)

`CLAUDE.md`, `README.md`, `docs/02_CRITERIOS_DE_ELEGIBILIDADE.md`, `docs/04_PIPELINE_E_STATUS.md`,
`.claude/agents/opportunity-discovery.md`, `.claude/agents/edital-validator.md`,
`.claude/agents/dhara-fit-scorer.md`, `.claude/agents/edital-reporter.md`.

### Removido (1)

`.claude/agents/edital-orchestrator.md`

## Passo a passo no GitHub web

### 1. Criar a branch

1. Abra o repositório em `github.com`.
2. Clique no seletor de branch (onde aparece `main`).
3. Digite `radar/v4.2-completo`.
4. Clique em "Create branch: radar/v4.2-completo from main".
5. Confirme que o seletor agora mostra `radar/v4.2-completo`. Todos os passos seguintes acontecem nessa branch.

### 2. Subir os arquivos que não estão em pastas ocultas (16 arquivos)

1. Descompacte `radar-editais-v4.2-arquivos.zip` no seu computador.
2. Na branch, clique em "Add file" → "Upload files".
3. Arraste as pastas `config/`, `docs/`, `templates/`, `data/` e os arquivos `CLAUDE.md` e `README.md`.
   O GitHub preserva a estrutura de pastas do que você arrasta.
4. Em "Commit changes", escolha "Commit directly to the radar/v4.2-completo branch".
5. Mensagem sugerida: `Radar v4.2: docs, config, templates e dados`.
6. Clique em "Commit changes".

Observações:
- Subir um arquivo com caminho já existente substitui o conteúdo. É o comportamento desejado para
  `CLAUDE.md`, `README.md`, `docs/02` e `docs/04`.
- Se `data/inbox/.gitkeep` e companhia não aparecerem no arrasto (arquivos que começam com ponto
  ficam ocultos no Finder e no Explorer), crie-os pelo passo 3.

### 3. Criar os arquivos de caminho oculto (4 agentes e, se preciso, os .gitkeep)

O upload por arrasto costuma não enxergar a pasta `.claude`. Use o editor:

1. Na branch, clique em "Add file" → "Create new file".
2. No campo do nome, digite o caminho completo, por exemplo:
   `.claude/agents/opportunity-discovery.md`
   Ao digitar a barra, o GitHub cria a pasta automaticamente.
3. Cole o conteúdo do arquivo correspondente do zip.
4. Commit na branch `radar/v4.2-completo`.
5. Repita para:
   - `.claude/agents/edital-validator.md`
   - `.claude/agents/dhara-fit-scorer.md`
   - `.claude/agents/edital-reporter.md`
6. Se os `.gitkeep` não subiram no passo 2, repita o mesmo processo para
   `data/inbox/.gitkeep`, `data/validated/.gitkeep`, `data/reports/.gitkeep` e `data/archive/.gitkeep`,
   deixando o conteúdo vazio ou com uma linha de comentário.

Atenção: esses quatro arquivos de agente já existem no repositório. Ao digitar o caminho de um arquivo
existente, o GitHub avisa que o arquivo já existe. Nesse caso, abra o arquivo existente, clique no lápis,
apague todo o conteúdo e cole a versão nova.

### 4. Remover o agente orquestrador

1. Abra `.claude/agents/edital-orchestrator.md` na branch.
2. Clique no ícone de lixeira ("Delete this file").
3. Mensagem sugerida: `Remove agente orquestrador; lógica movida para docs/06`.
4. Commit na branch `radar/v4.2-completo`.

### 5. Validar antes de abrir a PR

Use o checklist da seção "Checklist de validação" abaixo.

### 6. Abrir a Pull Request

1. Vá em "Pull requests" → "New pull request".
2. Base: `main`. Compare: `radar/v4.2-completo`.
3. Título: `Radar v4.2: agentes, operação e Notion com governança`
4. Descrição: copie o texto da seção "Descrição da Pull Request".
5. Clique em "Create pull request".
6. **Não faça merge.** Revise a aba "Files changed" antes de qualquer decisão.

## Checklist de validação

Marque na aba "Files changed" da PR e navegando pela branch:

- [ ] `.claude/agents/` tem exatamente quatro arquivos: `opportunity-discovery.md`, `edital-validator.md`, `dhara-fit-scorer.md`, `edital-reporter.md`
- [ ] `.claude/agents/edital-orchestrator.md` não existe mais
- [ ] `.claude/settings.json` não existe
- [ ] `docs/06_ORQUESTRACAO_DA_RODADA.md` existe
- [ ] `docs/07_NOTION_OPERACAO.md` existe
- [ ] `config/sources.yaml`, `config/scoring.yaml` e `config/notion.yaml` existem
- [ ] `templates/` tem `daily-report.md`, `weekly-report.md` e `opportunity-record.md`
- [ ] `data/` tem `inbox/`, `validated/`, `reports/` e `archive/`, cada uma com `.gitkeep`
- [ ] Em `config/notion.yaml`, a linha `habilitada: false` aparece em `sincronizacao`
- [ ] Em `config/notion.yaml`, `schema_verificado: false` e todos os `database_id` e `data_source_id` estão `null`
- [ ] Em `config/sources.yaml`, a fonte `prosas` tem `prioridade_descoberta: alta` e `url: null`
- [ ] Em `config/scoring.yaml`, `status: proposta_calibravel`
- [ ] A PR mostra 21 arquivos alterados: 12 adicionados, 8 modificados, 1 removido
- [ ] Nos diffs de `CLAUDE.md` e `README.md`, nada que você queria manter foi perdido

## Descrição da Pull Request

```markdown
Consolida a arquitetura do Radar de Editais — Dhara / IFA Records.

## Arquitetura

O repositório é a fonte de verdade das regras, agentes, critérios, fontes, templates e configurações.
A sessão principal do Claude Code é a orquestradora: ela delega as etapas, normaliza e deduplica os
registros, consolida o resultado e é a única responsável por escrever no Notion.

Sequência da rodada:
1. opportunity-discovery
2. edital-validator
3. normalização e deduplicação pela sessão principal
4. dhara-fit-scorer
5. edital-reporter
6. consolidação pela sessão principal
7. sincronização com o Notion, com confirmação humana

## Subagentes

Quatro subagentes formais, em `.claude/agents/`: descoberta, validação, score e relatório.
O antigo `edital-orchestrator` foi removido: no Claude Code um subagente não pode criar outros
subagentes. A lógica de orquestração virou `docs/06_ORQUESTRACAO_DA_RODADA.md`.
O `edital-reporter` passa a gravar relatórios e payloads apenas em `data/reports/`.
Nenhum subagente tem acesso ao Notion.

## Notion

O Notion é a camada operacional de registro (`docs/07_NOTION_OPERACAO.md`): pipeline de oportunidades,
relatórios e histórico incremental. Entra desabilitado: `config/notion.yaml` tem os IDs nulos,
`schema_verificado: false` e `sincronizacao.habilitada: false`. Antes da primeira sincronização real há
um procedimento de conexão com ambiente de teste e validação de deduplicação.

## Três níveis de atualização

- Factual: prazos, status validado e operacional, valores, links, score, confiança, prioridade, revisão,
  próxima ação, última validação e acréscimos de evidência e histórico; movimentos objetivos do funil.
- Estratégica: Decisão para APLICAR, AVALIAR_COM_PARCERIA ou DESCARTAR e Status do funil para APLICAR,
  AVALIAR_COM_PARCERIA, DESCARTADO, EM_PREPARACAO ou PRONTO_PARA_INSCRICAO. Exigem prévia completa
  (valor atual e proposto, motivo, evidência, URL, impacto, trecho de histórico e payload exato) e
  aprovação explícita.
- Exclusivamente humana: INSCRITO, RESULTADO_AGUARDADO, APROVADO, NAO_APROVADO, Responsável,
  Notas humanas e dados sensíveis.

Toda escrita no Notion passa pela permissão da ferramenta; `notion-create-pages` e `notion-update-page`
nunca são pré-aprovadas.

## Prazo vencido em preparação

Para registros em EM_PREPARACAO ou PRONTO_PARA_INSCRICAO com edital encerrado ou prazo vencido:
os campos factuais são atualizados de imediato (status validado e operacional, prioridade REVISAO,
revisão humana, última validação, evidência e histórico), o funil, a Decisão, o Responsável e os campos
de inscrição e resultado são preservados, e o relatório abre um alerta crítico com proposta estratégica
por oportunidade.

## Fora do escopo desta PR

`.claude/settings.json` (proteção técnica de arquivos) vem em PR separada, depois da rodada piloto.
```

## Diffs dos 8 arquivos modificados

Para conferência. No GitHub web, o mais simples é substituir o conteúdo pelo arquivo final do zip; estes
diffs servem para você revisar o que muda.

### CLAUDE.md

```diff
@@ -1,5 +1,5 @@
 # CLAUDE.md — Radar de Editais da Dhara / IFA Records
 
-Estas são as instruções permanentes para qualquer sessão, tarefa ou subagente que trabalhe neste repositório. Leia este arquivo antes de analisar, pesquisar, criar, editar ou executar qualquer fluxo.
+Estas são as instruções permanentes para qualquer sessão, tarefa ou subagente que trabalhe neste repositório. A sessão principal do Claude Code é a orquestradora do radar. Leia este arquivo antes de analisar, pesquisar, criar, editar ou executar qualquer fluxo.
 
 ## Missão
@@ -9,4 +9,6 @@ Este repositório opera um radar de oportunidades culturais para Dhara Guimarãe
 O radar descobre, valida, classifica, prioriza e acompanha editais, chamamentos públicos, prêmios, residências, festivais, showcases, oportunidades de circulação, intercâmbio e outras chamadas culturais. O objetivo é apoiar decisão humana e preparação de candidaturas; não é realizar inscrições automaticamente.
 
+O repositório é a fonte de verdade das regras, agentes, critérios, fontes, templates e configurações. O Notion é o sistema de registro operacional (pipeline, relatórios e histórico), conforme `docs/07_NOTION_OPERACAO.md`.
+
 ## Contexto fixo
 
@@ -58,4 +60,6 @@ Use esta ordem para resolver conflitos e validar afirmações:
 - Não tratar uma página existente como prova de inscrições abertas. Confirmar prazo futuro, status explícito, formulário ativo ou comunicação oficial recente.
 - Preservar editais encerrados no histórico somente quando forem relevantes à rastreabilidade; não recomendá-los para candidatura.
+- Não editar `config/sources.yaml` automaticamente. URLs sugeridas para fontes com `url: null` entram no relatório como proposta e dependem de validação humana. Nunca inventar URL.
+- A PROSAS é fonte prioritária de descoberta no Brasil, mas não pode ser a única evidência de status, prazo, valor ou elegibilidade quando houver regulamento ou fonte organizadora disponível.
 
 ## Escopo de oportunidades
@@ -82,5 +86,5 @@ Descartar ou marcar baixa prioridade, salvo ordem humana contrária:
 ## Pipeline e decisões
 
-Use os status definidos em `docs/04_PIPELINE_E_STATUS.md`. As decisões analíticas são:
+Use os status definidos em `docs/04_PIPELINE_E_STATUS.md`. Todos os valores internos (status do funil, status da chamada, decisões e prioridades) são escritos sem espaço e sem acento; nos relatórios, exibir os rótulos legíveis definidos nesse documento. As decisões analíticas usam exatamente estes valores internos:
 
 | Decisão | Definição |
@@ -110,10 +114,11 @@ Aplicar penalidades justificadas para prazo insuficiente, status não confirmado
 Nunca ocultar a incerteza dentro de um score. Sempre retornar também `confidence_score` entre 0 e 1, riscos e pendências.
 
-## Subagentes e delegação
+## Orquestração e subagentes
+
+A **sessão principal do Claude Code** é a orquestradora do radar. Ela lê este arquivo e `docs/06_ORQUESTRACAO_DA_RODADA.md`, delega as etapas aos subagentes e consolida o resultado. Não existe subagente orquestrador: no Claude Code, subagentes não podem criar outros subagentes.
 
-Antes de uma rodada operacional, verificar a existência e legibilidade dos seguintes arquivos:
+Subagentes formais, em `.claude/agents/`:
 
 ```text
-.claude/agents/edital-orchestrator.md
 .claude/agents/opportunity-discovery.md
 .claude/agents/edital-validator.md
@@ -122,19 +127,30 @@ Antes de uma rodada operacional, verificar a existência e legibilidade dos segu
 ```
 
-Fluxo obrigatório:
+Sequência obrigatória, delegada pela sessão principal:
 
 ```text
-1. opportunity-discovery
-2. edital-validator
-3. dhara-fit-scorer
-4. edital-reporter
-5. edital-orchestrator consolida resultados e estado operacional
+1. opportunity-discovery   → descoberta de candidatas
+2. edital-validator        → validação em fonte oficial
+3. sessão principal        → normalização e deduplicação
+4. dhara-fit-scorer        → score, decisão e riscos
+5. edital-reporter         → alertas, relatório em data/reports/ e payloads do Notion
+6. sessão principal        → consolidação e estado operacional
+7. sessão principal        → sincronização com o Notion, com confirmação humana
 ```
 
-- O orquestrador deve delegar, quando o ambiente suportar subagentes.
+- Antes de uma rodada, confirmar que os quatro subagentes estão disponíveis (por exemplo, com `/agents`).
+- Ler as instruções específicas de cada subagente antes de delegar sua tarefa.
 - Se um subagente necessário estiver ausente, inválido ou não for suportado pelo ambiente atual, declarar a limitação de forma explícita.
 - Não fingir que uma delegação ocorreu quando ela não ocorreu.
 - Somente usar modo de agente único se a pessoa usuária autorizar expressamente; nesse caso, manter a mesma sequência lógica e identificar a saída como `modo_agente_unico`.
-- Ler as instruções específicas de cada agente antes de delegar sua tarefa.
+- Consolidar sem alterar dados, score, evidências ou conclusões dos subagentes.
+- Nenhum subagente acessa o Notion. Não adicionar ferramentas MCP do Notion ao campo `tools` de nenhum arquivo em `.claude/agents/`.
+
+### Permissões de escrita local
+
+- `edital-reporter`: pode criar relatórios e payloads do Notion somente em `data/reports/`.
+- Sessão principal: grava em `data/inbox/`, `data/validated/` e `data/archive/` somente quando a pessoa usuária pedir explicitamente para registrar histórico; grava o log de sincronização `data/reports/AAAA-MM-DD-sync-notion.md`.
+- Demais subagentes: somente leitura e pesquisa.
+- Alterações em `CLAUDE.md`, `README.md`, `docs/`, `config/`, `templates/` e `.claude/` exigem plano prévio e aprovação humana.
 
 ## Operação e relatórios
@@ -142,21 +158,26 @@ Fluxo obrigatório:
 ### Ordem da rodada
 
-1. Ler este arquivo, `docs/`, `config/` e estado/relatório mais recente.
-2. Descobrir candidatas em fontes permitidas.
-3. Validar status, fonte oficial, prazo e regras.
-4. Normalizar e deduplicar os registros.
-5. Analisar elegibilidade, riscos, score e decisão.
-6. Produzir alertas e relatório diário.
-7. Atualizar base externa apenas se houver conexão, permissão e instruções específicas.
+Preparação — sessão principal: ler este arquivo, `docs/`, `config/` e o relatório mais recente em `data/reports/`; definir o escopo.
+
+1. `opportunity-discovery`: descobrir candidatas em fontes permitidas e propor URLs para fontes com `url: null`.
+2. `edital-validator`: validar status, fonte oficial, prazo e regras; atribuir `status_validado` e `status_operacional`.
+3. Sessão principal: normalizar e deduplicar os registros.
+4. `dhara-fit-scorer`: analisar elegibilidade, riscos, score e decisão.
+5. `edital-reporter`: produzir alertas e relatório diário, gravado em `data/reports/`, e preparar payloads do Notion.
+6. Sessão principal: consolidar.
+7. Sessão principal: sincronizar com o Notion conforme `docs/07_NOTION_OPERACAO.md`, somente com IDs resolvidos, schema verificado e aprovação humana. Se o Notion estiver inacessível, a rodada termina normalmente e a falha fica registrada.
 
 ### Alertas
 
-- URGENTE: status aberto validado + decisão APLICAR ou AVALIAR_COM_PARCERIA + prazo de até 7 dias.
-- ALTA_PRIORIDADE: score >= 75 + status aberto validado + confiança >= 0,70.
-- REVISAO: dado crítico ausente, divergência de fonte, dúvida sobre elegibilidade, requisito de parceiro/anfitrião, exigência de visto/idioma ou pendência documental.
+Valores internos padronizados: `URGENTE`, `ALTA_PRIORIDADE`, `REVISAO`. Regras completas em `docs/04_PIPELINE_E_STATUS.md`.
+
+- `URGENTE`: `status_operacional` igual a `ABERTA` + decisão `APLICAR` ou `AVALIAR_COM_PARCERIA` + prazo de até 7 dias. Os três critérios são obrigatórios. Uma chamada `PRORROGADA` com fonte oficial, prazo futuro inequívoco e inscrição confirmada tem `status_operacional` = `ABERTA` e pode ser `URGENTE`.
+- `ALTA_PRIORIDADE`: score >= 75 + `status_operacional` igual a `ABERTA` + confiança >= 0,70.
+- `REVISAO`: dado crítico ausente, divergência de fonte, dúvida sobre elegibilidade, requisito de parceiro/anfitrião, exigência de visto/idioma ou pendência documental.
 
 ### Formato de comunicação
 
 - Escrever em português do Brasil.
+- Seguir os modelos em `templates/`.
 - Ser objetiva, precisa e transparente sobre incertezas.
 - Informar prazo com data, horário e fuso quando conhecidos.
@@ -166,9 +187,19 @@ Fluxo obrigatório:
 ## Notion e sistemas externos
 
-- O Notion é opcional e serve como pipeline operacional, não como fonte de decisão.
-- Não criar, editar ou apagar páginas/registros externos sem instrução explícita e autorização quando requerida.
-- Antes de gravar no Notion, confirmar qual database deve ser usada e quais campos podem ser preenchidos.
-- Quando autorizado, registrar preferencialmente itens APLICAR, AVALIAR_COM_PARCERIA e MONITORAR com URLs, evidências, prazo, score, decisão e próxima ação.
-- Não alterar status como INSCRITO, APROVADO ou NÃO_APROVADO sem informação humana explícita.
+O Notion é o sistema de registro operacional do radar: pipeline de oportunidades (`Pipeline de Editais — IFA Records`), relatórios (`Relatórios do Radar — IFA Records`) e histórico de alterações. Ele não é fonte de decisão nem de regras. A especificação completa está em `docs/07_NOTION_OPERACAO.md`.
+
+- Somente a sessão principal lê e grava no Notion. Subagentes nunca acessam o Notion; o `edital-reporter` apenas prepara payloads.
+- Antes de qualquer escrita: IDs resolvidos em `config/notion.yaml`, schema verificado na rodada, consulta de deduplicação, apresentação do conteúdo exato e aprovação humana.
+- Gravar oportunidades somente depois de descoberta, validação (ou registro explícito de fonte oficial não localizada), score e decisão final, e somente com decisão `APLICAR`, `AVALIAR_COM_PARCERIA` ou `MONITORAR`.
+- Usar a chave de deduplicação definida em `docs/07`. Nunca criar duplicatas e nunca apagar, arquivar ou enviar registros para a lixeira.
+- Nunca sobrescrever evidências históricas: toda mudança acrescenta uma entrada ao histórico da página, com data/hora, fonte e trecho.
+- Atualizações seguem três níveis definidos em `docs/07` e `config/notion.yaml`:
+  - **Factual**: prazos, status validado/operacional, valores, links, score, confiança, prioridade, revisão, próxima ação, última validação e acréscimos de evidência e histórico; Status do funil para `EM_VALIDACAO`, `AGUARDANDO_REVISAO_HUMANA`, `ENCERRADO` ou `MONITORAR` somente por gatilho objetivo. Gravadas sem prévia estratégica, mas sempre pela permissão da ferramenta.
+  - **Estratégica**: Decisão para `APLICAR`, `AVALIAR_COM_PARCERIA` ou `DESCARTAR`; Status do funil para `APLICAR`, `AVALIAR_COM_PARCERIA`, `DESCARTADO`, `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`; qualquer mudança quando o funil estiver em `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`. Exigem prévia completa e aprovação explícita antes de gravar.
+  - **Prazo vencido em candidatura em preparação**: com o funil em `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO` e o edital encerrado ou o prazo vencido, atualizar de imediato status validado e operacional, prioridade `REVISAO`, revisão humana, última validação e histórico; nunca alterar funil, Decisão, Responsável ou campos de inscrição e resultado; emitir alerta crítico e proposta estratégica por oportunidade.
+  - **Exclusivamente humana**: `INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO`, `NAO_APROVADO`, Responsável, Notas humanas, dados bancários ou fiscais, documentos, declarações, contratos e anexos sensíveis. O radar nunca grava esses itens.
+- Relatórios no Notion são sempre páginas novas; páginas anteriores não são editadas.
+- Não alterar schema, views ou estrutura das databases durante a operação.
+- Se o Notion estiver inacessível, continuar a rodada e registrar a falha de sincronização no relatório.
 - Não transmitir documentos empresariais, dados pessoais sensíveis, credenciais, dados bancários ou certidões para ferramentas externas.
 
@@ -204,6 +235,12 @@ docs/03_FONTES_DE_MONITORAMENTO.md
 docs/04_PIPELINE_E_STATUS.md
 docs/05_KIT_DOCUMENTAL.md
+docs/06_ORQUESTRACAO_DA_RODADA.md
+docs/07_NOTION_OPERACAO.md
 config/sources.yaml
 config/scoring.yaml
+config/notion.yaml
+templates/daily-report.md
+templates/weekly-report.md
+templates/opportunity-record.md
 ```
 
@@ -219,7 +256,7 @@ Se for a primeira sessão ou se houver dúvida de configuração:
 
 1. Liste os arquivos relevantes encontrados.
-2. Confirme os subagentes disponíveis e o ambiente em uso.
+2. Confirme os quatro subagentes disponíveis e o ambiente em uso.
 3. Identifique lacunas de configuração, fontes e credenciais.
 4. Não comece uma coleta ou faça alterações externas sem confirmação de escopo quando ele não estiver claro.
 
-Para uma rodada de pesquisa, a regra padrão é: executar apenas descoberta, validação, classificação e relatório; não tomar ações externas.
+Para uma rodada de pesquisa, a regra padrão é: executar descoberta, validação, classificação e relatório. A única ação externa prevista é a sincronização com o Notion descrita em `docs/07`, sempre com aprovação humana.
```

### README.md

```diff
@@ -3,5 +3,5 @@
 Sistema orientado por agentes Claude para descobrir, validar, priorizar e acompanhar editais, chamadas públicas, festivais, residências e oportunidades culturais para Dhara Guimarães, artista do casting da IFA Sounds, cujo nome comercial é IFA Records.
 
-O repositório é a fonte de verdade das regras do radar: perfil artístico, critérios de elegibilidade, fontes monitoradas, pipeline operacional, instruções dos subagentes e decisões técnicas. O Claude Code lê essas instruções e coordena os agentes especializados; o Notion pode ser usado opcionalmente como painel de acompanhamento humano.
+O repositório é a fonte de verdade das regras do radar: perfil artístico, critérios de elegibilidade, fontes monitoradas, pipeline operacional, instruções dos subagentes e decisões técnicas. A sessão principal do Claude Code lê essas instruções, orquestra a rodada e delega as etapas a quatro subagentes especializados. O Notion é a camada operacional de registro: pipeline de oportunidades, relatórios e histórico, sincronizados somente pela sessão principal e com aprovação humana.
 
 Este projeto monitora e organiza oportunidades. Ele não realiza automaticamente inscrições, assinaturas, pagamentos, envios de documentos, contratações ou outras ações irreversíveis.
@@ -68,4 +68,6 @@ A Dhara pode desenvolver, apresentar e circular projetos no Brasil inteiro e int
 ## Decisões do radar
 
+Todos os valores internos (decisões, prioridades e status do funil) são escritos sem espaço e sem acento, por exemplo `EM_VALIDACAO` e `NAO_APROVADO`. Os relatórios exibem rótulos legíveis, como "Em validação" e "Não aprovado". A tabela completa está em `docs/04_PIPELINE_E_STATUS.md`.
+
 | Decisão | Quando usar |
 |---|---|
@@ -86,8 +88,9 @@ radar-editais-dhara/
 │   ├── 03_FONTES_DE_MONITORAMENTO.md
 │   ├── 04_PIPELINE_E_STATUS.md
-│   └── 05_KIT_DOCUMENTAL.md
+│   ├── 05_KIT_DOCUMENTAL.md
+│   ├── 06_ORQUESTRACAO_DA_RODADA.md
+│   └── 07_NOTION_OPERACAO.md
 ├── .claude/
 │   └── agents/
-│       ├── edital-orchestrator.md
 │       ├── opportunity-discovery.md
 │       ├── edital-validator.md
@@ -101,5 +104,6 @@ radar-editais-dhara/
 ├── config/
 │   ├── sources.yaml
-│   └── scoring.yaml
+│   ├── scoring.yaml
+│   └── notion.yaml
 └── templates/
     ├── daily-report.md
@@ -112,48 +116,53 @@ radar-editais-dhara/
 | Caminho | Finalidade |
 |---|---|
-| `CLAUDE.md` | Regras globais que o Claude deve seguir em todas as sessões no repositório. |
-| `docs/` | Contexto de negócio e regras operacionais detalhadas. |
-| `.claude/agents/` | Definições individuais dos subagentes. Cada arquivo representa um agente especializado. |
+| `CLAUDE.md` | Regras globais que o Claude deve seguir em todas as sessões no repositório; define a sessão principal como orquestradora. |
+| `docs/` | Contexto de negócio e regras operacionais detalhadas. `docs/06_ORQUESTRACAO_DA_RODADA.md` descreve a rodada conduzida pela sessão principal; `docs/07_NOTION_OPERACAO.md` define o uso do Notion. |
+| `.claude/agents/` | Definições dos quatro subagentes formais. Cada arquivo representa um agente especializado. |
 | `config/sources.yaml` | Lista versionada de fontes, frequência, categoria e nível de autoridade. |
 | `config/scoring.yaml` | Pesos e regras configuráveis do score de aderência. |
-| `data/` | Dados de trabalho, relatórios e histórico. Evitar versionar informações confidenciais. |
+| `config/notion.yaml` | IDs das databases do Notion e chave que habilita a sincronização. Sem segredos. |
+| `data/` | Dados de trabalho: `inbox/`, `validated/`, `reports/` e `archive/`. Evitar versionar informações confidenciais. |
 | `templates/` | Modelos de saídas padronizadas. |
 
 ## Agentes
 
-O sistema é organizado em agentes especializados, coordenados pelo orquestrador.
+A sessão principal do Claude Code é a orquestradora. Ela não é um subagente: no Claude Code, subagentes não podem criar outros subagentes. As regras da orquestração estão em `CLAUDE.md` e `docs/06_ORQUESTRACAO_DA_RODADA.md`.
 
-| Agente | Arquivo | Responsabilidade |
+| Papel | Quem executa / arquivo | Responsabilidade |
 |---|---|---|
-| Orquestrador | `.claude/agents/edital-orchestrator.md` | Confere pré-condições, chama os demais agentes na ordem correta e consolida a execução. |
+| Orquestração | Sessão principal (`CLAUDE.md`, `docs/06_ORQUESTRACAO_DA_RODADA.md`, `docs/07_NOTION_OPERACAO.md`) | Confere pré-condições, delega aos subagentes na ordem correta, normaliza e deduplica registros, consolida a execução e é a única que sincroniza com o Notion. |
 | Descoberta | `.claude/agents/opportunity-discovery.md` | Localiza editais e oportunidades candidatas no Brasil e exterior. |
 | Validação | `.claude/agents/edital-validator.md` | Confere fonte oficial, regulamento, status, prazo, valor, exigências e evidências. |
 | Elegibilidade e score | `.claude/agents/dhara-fit-scorer.md` | Avalia aderência à Dhara/IFA, riscos, pendências e recomendação. |
-| Relatórios e alertas | `.claude/agents/edital-reporter.md` | Produz alertas, relatório diário e revisão semanal. |
+| Relatórios e alertas | `.claude/agents/edital-reporter.md` | Produz alertas, relatório diário e revisão semanal e prepara payloads do Notion; pode gravar somente em `data/reports/` e não acessa o Notion. |
 
 ### Ordem obrigatória de execução
 
 ```text
-1. opportunity-discovery
-2. edital-validator
-3. dhara-fit-scorer
-4. edital-reporter
-5. edital-orchestrator consolida o resultado
+1. opportunity-discovery   (subagente)
+2. edital-validator        (subagente)
+3. normalização e deduplicação pela sessão principal
+4. dhara-fit-scorer        (subagente)
+5. edital-reporter         (subagente)
+6. consolidação pela sessão principal
+7. sincronização com o Notion pela sessão principal, com aprovação humana
 ```
 
-O orquestrador não deve simular agentes ausentes. Antes de iniciar uma rodada, ele deve verificar se todos os arquivos necessários existem e se o frontmatter de cada subagente é reconhecido pelo ambiente Claude em uso.
+A sessão principal não deve simular agentes ausentes. Antes de iniciar uma rodada, ela deve verificar se todos os arquivos necessários existem e se os quatro subagentes aparecem em `/agents`.
 
 ## Fluxo de uma rodada
 
-1. O orquestrador lê `CLAUDE.md`, os documentos em `docs/`, a configuração de fontes e o último relatório disponível.
+1. A sessão principal lê `CLAUDE.md`, os documentos em `docs/`, `config/` e o último relatório em `data/reports/`.
 2. O agente de descoberta pesquisa fontes permitidas e registra oportunidades candidatas com URLs e evidências iniciais.
 3. O agente de validação localiza a fonte oficial e o regulamento, confirma ou invalida status/prazo e extrai regras estruturadas.
-4. O agente de elegibilidade calcula score, registra riscos e decide entre aplicar, avaliar parceria, monitorar ou descartar.
-5. O agente de relatório produz alertas e um relatório em português do Brasil.
-6. Se o Notion estiver conectado e autorizado, apenas os itens aprovados para acompanhamento podem ser registrados no pipeline, sem qualquer submissão automática.
+4. A sessão principal normaliza e deduplica os registros validados.
+5. O agente de elegibilidade calcula score, registra riscos e decide entre aplicar, avaliar parceria, monitorar ou descartar.
+6. O agente de relatório produz alertas e um relatório em português do Brasil, gravado em `data/reports/`.
+7. A sessão principal consolida o resultado.
+8. Se a sincronização estiver habilitada em `config/notion.yaml`, a sessão principal verifica o schema, deduplica, apresenta o conteúdo exato, grava no Notion somente o que for aprovado e cria a página do relatório. Se o Notion estiver inacessível, a falha é registrada e a rodada termina normalmente.
 
 ## Critérios de prioridade
 
-O score de aderência varia de 0 a 100 e deve ser explicável. A configuração detalhada deve ficar em `config/scoring.yaml`.
+O score de aderência varia de 0 a 100 e deve ser explicável. A configuração detalhada fica em `config/scoring.yaml`.
 
 | Critério | Pontuação máxima |
@@ -183,5 +192,5 @@ Aplicar penalidades explícitas por status não confirmado, edital encerrado, im
 ### Status aberto
 
-Uma oportunidade só pode ser marcada como ABERTA se houver evidência atual de pelo menos um dos itens abaixo:
+Uma oportunidade só pode ser marcada como `ABERTA` se houver evidência atual de pelo menos um dos itens abaixo:
 
 - Prazo futuro inequívoco em fonte oficial.
@@ -190,4 +199,6 @@ Uma oportunidade só pode ser marcada como ABERTA se houver evidência atual de
 - Comunicação institucional recente que confirme abertura ou prorrogação.
 
+Uma chamada `PRORROGADA` mantém esse valor em `status_validado` (histórico) e passa a ter `status_operacional` = `ABERTA` quando houver fonte oficial, prazo futuro inequívoco e inscrição disponível ou confirmada. As decisões e alertas usam o `status_operacional`. Detalhes em `docs/04_PIPELINE_E_STATUS.md`.
+
 Quando prazo, horário, fuso, elegibilidade, valor ou regulamento não forem encontrados, o agente deve declarar o campo como não localizado, reduzir a confiança e marcar revisão humana. Nunca preencher lacunas por suposição.
 
@@ -204,41 +215,27 @@ O radar deve procurar, validar e acompanhar oportunidades de:
 - Chamadas que aceitem artistas brasileiros, pessoas jurídicas brasileiras, coproduções ou parceiros anfitriões.
 
-A lista operacional de fontes deve ser mantida em `config/sources.yaml`. Uma fonte agregadora pode disparar descoberta, mas não pode ser a única base para afirmar que uma oportunidade está aberta ou elegível.
+A lista operacional de fontes é mantida em `config/sources.yaml`. URLs ainda não verificadas ficam como `null`; o radar pode sugerir URLs no relatório, mas não edita o arquivo automaticamente. Uma fonte agregadora pode disparar descoberta, mas não pode ser a única base para afirmar que uma oportunidade está aberta ou elegível.
 
-## Notion opcional
+## Notion como camada operacional
 
-O Notion é uma camada de acompanhamento, não o motor de decisão. Use-o para registrar itens que passaram pela análise e exigem ação humana.
+O repositório continua sendo a fonte de verdade das regras. O Notion é o sistema de registro operacional: pipeline de oportunidades, relatórios diários e semanais e histórico de alterações. A especificação completa está em `docs/07_NOTION_OPERACAO.md`.
 
-### Banco sugerido
-
-Nome: **Pipeline de Editais — IFA Records**
+| Database | Conteúdo |
+|---|---|
+| `Pipeline de Editais — IFA Records` | Uma página por oportunidade com decisão `APLICAR`, `AVALIAR_COM_PARCERIA` ou `MONITORAR`. Propriedades guardam o valor atual; o corpo da página guarda evidências e histórico de alterações. |
+| `Relatórios do Radar — IFA Records` | Uma página nova por relatório diário ou semanal, relacionada às oportunidades da rodada. |
 
-Propriedades recomendadas:
+Regras principais:
 
-- Edital / oportunidade
-- Status
-- Decisão
-- Score
-- Urgência
-- Instituição
-- País
-- Estado/região
-- Modalidade
-- Prazo
-- Moeda
-- Valor máximo
-- PJ aceita?
-- Exige parceiro local?
-- Fonte oficial confirmada?
-- Confiança
-- Link oficial
-- Regulamento
-- Próxima ação
-- Responsável
-- Revisão humana necessária?
-- Última validação
-- Observações e evidências
+- Somente a sessão principal lê e grava no Notion; os subagentes não têm acesso. O `edital-reporter` apenas prepara payloads.
+- Toda escrita exige IDs resolvidos em `config/notion.yaml`, schema verificado, consulta de deduplicação, apresentação do conteúdo exato e aprovação humana.
+- A chave de deduplicação é a URL canônica da página oficial ou o identificador externo da chamada. O radar nunca cria duplicatas e nunca apaga registros.
+- Evidências históricas nunca são sobrescritas: cada mudança acrescenta uma entrada ao histórico da página.
+- Atualizações factuais (prazos, status da chamada, valores, links, score, prioridade e movimentos objetivos do funil) são gravadas sem prévia estratégica. Mudanças estratégicas de Decisão ou Status do funil (Aplicar, Avaliar com parceria, Descartar, Em preparação, Pronto para inscrição) exigem prévia e aprovação explícita.
+- O radar nunca define `INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO` ou `NAO_APROVADO`, nem altera Responsável, Notas humanas ou dados sensíveis.
+- Se o Notion estiver inacessível, a rodada continua e a falha fica registrada no relatório.
+- As permissões locais de `.claude/settings.json` não controlam o Notion.
 
-Antes de permitir criação ou atualização no Notion, estabeleça explicitamente quais campos o Claude pode editar. Não autorize o Claude a mudar INSCRITO, APROVADO, NÃO_APROVADO ou dados sensíveis sem uma decisão humana explícita.
+Antes da primeira sincronização real, siga o procedimento "Primeira conexão operacional" de `docs/07_NOTION_OPERACAO.md`.
 
 ## Como operar no Claude
@@ -247,8 +244,9 @@ Antes de permitir criação ou atualização no Notion, estabeleça explicitamen
 
 1. Confirme que `CLAUDE.md` está na raiz do repositório.
-2. Confirme que os cinco documentos em `docs/` existem e estão atualizados.
-3. Confirme que cada agente existe em `.claude/agents/` e possui frontmatter YAML válido.
-4. Configure ou revise `config/sources.yaml` e `config/scoring.yaml`.
-5. Execute uma rodada piloto, sem alterações externas e sem Notion.
+2. Confirme que os sete documentos em `docs/` existem e estão atualizados.
+3. Confirme que os quatro subagentes existem em `.claude/agents/`, possuem frontmatter YAML válido e aparecem em `/agents`.
+4. Configure ou revise `config/sources.yaml` e `config/scoring.yaml`, e confira os modelos em `templates/`.
+5. Execute uma rodada piloto, sem alterações externas e sem Notion (`sincronizacao.habilitada: false` em `config/notion.yaml`).
+6. Siga a "Primeira conexão operacional" de `docs/07_NOTION_OPERACAO.md` antes de habilitar a sincronização.
 
 ### Prompt de auditoria inicial
@@ -265,5 +263,5 @@ Confirme:
 2. Se cada arquivo possui frontmatter reconhecível pelo ambiente atual.
 3. Se há arquivos, regras ou configurações ausentes.
-4. A ordem correta de delegação do orquestrador.
+4. A ordem de delegação da sessão principal, conforme docs/06_ORQUESTRACAO_DA_RODADA.md.
 5. Quais dados ainda precisam ser fornecidos manualmente antes da primeira rodada real.
 
@@ -274,5 +272,5 @@ Se encontrar problemas, apresente apenas um plano de correção e patches sugeri
 
 ```text
-Execute uma rodada piloto do Radar de Editais — Dhara / IFA Records.
+Execute uma rodada piloto do Radar de Editais — Dhara / IFA Records, seguindo docs/06_ORQUESTRACAO_DA_RODADA.md e delegando aos quatro subagentes.
 
 Escopo:
@@ -288,28 +286,34 @@ Restrições:
 - Não inventar dados ausentes.
 
-Entregue relatório diário em português do Brasil, com oportunidades urgentes, prioritárias, pendências e recomendações de próxima ação.
+Entregue relatório diário em português do Brasil, com oportunidades urgentes, prioritárias, pendências e recomendações de próxima ação. O edital-reporter pode gravá-lo em data/reports/.
 ```
 
 ## Relatórios e alertas
 
-### Alerta urgente
+Valores internos de prioridade: `URGENTE`, `ALTA_PRIORIDADE`, `REVISAO`. Regras completas em `docs/04_PIPELINE_E_STATUS.md`.
 
-Gerar alerta URGENTE quando:
+### URGENTE
 
-- A oportunidade estiver aberta e validada.
-- A decisão for APLICAR ou AVALIAR_COM_PARCERIA.
-- O prazo final estiver em até sete dias.
+Gerar alerta `URGENTE` somente quando os três critérios forem verdadeiros:
 
-### Alta prioridade
+- `status_operacional` igual a `ABERTA`, validado em fonte oficial (inclui chamada prorrogada com novo prazo e inscrição confirmados).
+- Decisão `APLICAR` ou `AVALIAR_COM_PARCERIA`.
+- Prazo final em até sete dias.
 
-Marcar ALTA PRIORIDADE quando:
+### ALTA_PRIORIDADE
+
+Marcar `ALTA_PRIORIDADE` quando:
 
 - O score for igual ou superior a 75.
-- O status aberto estiver confirmado.
+- `status_operacional` for `ABERTA`.
 - O nível de confiança for igual ou superior a 0,70.
 
+### REVISAO
+
+Marcar `REVISAO` quando houver dado crítico ausente, divergência de fonte, dúvida de elegibilidade, exigência de parceiro/anfitrião, visto, idioma ou cofinanciamento, ou prazo/fuso ambíguo.
+
 ### Relatório diário
 
-Deve incluir:
+Modelo: `templates/daily-report.md`. Deve incluir:
 
 - Urgentes.
@@ -322,5 +326,5 @@ Deve incluir:
 ### Relatório semanal
 
-Deve incluir:
+Modelo: `templates/weekly-report.md`. Deve incluir:
 
 - Pipeline por status e decisão.
@@ -345,10 +349,10 @@ Deve incluir:
 | Frequência | Atividade |
 |---|---|
-| Frequência | Atividade |
 | Diária, em dias úteis | Rodada de descoberta, validação, score e alertas. |
 | Semanal | Revisão de pipeline, prazos, parcerias e decisões de candidatura. |
 | Mensal | Atualização das fontes, pesos do score e kit documental. |
 | A cada edital prioritário | Criar uma pasta/dossiê de candidatura, checklist e versão adaptada do projeto. |
-| A cada alteração estrutural | Revisar `CLAUDE.md`, agentes e documentos de contexto. |
+| A cada alteração estrutural | Revisar `CLAUDE.md`, `docs/06_ORQUESTRACAO_DA_RODADA.md`, `docs/07_NOTION_OPERACAO.md`, subagentes e documentos de contexto. |
+| A cada mudança no schema do Notion | Atualizar `docs/07_NOTION_OPERACAO.md` e repetir a verificação de schema antes da próxima sincronização. |
 
 ## Estado atual do projeto
```

### docs/02_CRITERIOS_DE_ELEGIBILIDADE.md

```diff
@@ -37,5 +37,5 @@ Descartar, salvo instrução humana contrária:
 - Não restringir buscas a São Paulo.
 - Incluir chamadas estaduais, municipais, nacionais e internacionais.
-- Se a chamada exigir residência, sede ou CNPJ local, marcar “AVALIAR COM PARCERIA” se houver possibilidade prática de:
+- Se a chamada exigir residência, sede ou CNPJ local, marcar `AVALIAR_COM_PARCERIA` se houver possibilidade prática de:
   - Coprodução.
   - Parceiro local.
@@ -44,5 +44,5 @@ Descartar, salvo instrução humana contrária:
   - Convite de festival ou espaço cultural.
   - Projeto de circulação.
-- Marcar “DESCARTAR” apenas se a regra for inequivocamente impeditiva e não houver rota realista de participação.
+- Marcar `DESCARTAR` apenas se a regra for inequivocamente impeditiva e não houver rota realista de participação.
 
 ## Regras de fonte
@@ -60,11 +60,15 @@ Se houver divergência, o regulamento oficial mais recente e suas retificações
 ## Escala de decisão
 
-- APLICAR: alta aderência, status aberto confirmado e elegibilidade confirmada ou muito provável.
-- AVALIAR COM PARCERIA: alta ou média aderência, mas depende de parceiro, coprodutor, anfitrião, proponente local ou checagem jurídica/documental.
-- MONITORAR: oportunidade anunciada, futura, parcialmente aderente ou ainda com informação essencial ausente.
-- DESCARTAR: encerrada, incompatível, inelegível de modo evidente ou sem viabilidade operacional.
+Valores internos padronizados (usar exatamente esta grafia em registros, agentes e relatórios): `APLICAR`, `AVALIAR_COM_PARCERIA`, `MONITORAR`, `DESCARTAR`.
+
+- `APLICAR`: alta aderência, status aberto confirmado e elegibilidade confirmada ou muito provável.
+- `AVALIAR_COM_PARCERIA`: alta ou média aderência, mas depende de parceiro, coprodutor, anfitrião, proponente local ou checagem jurídica/documental.
+- `MONITORAR`: oportunidade anunciada, futura, parcialmente aderente ou ainda com informação essencial ausente.
+- `DESCARTAR`: encerrada, incompatível, inelegível de modo evidente ou sem viabilidade operacional.
 
 ## Score de aderência: 0 a 100
 
+Os pesos e penalidades operacionais ficam em `config/scoring.yaml`. Os valores abaixo são a referência de negócio; em caso de divergência, pedir revisão humana antes de alterar qualquer um dos dois.
+
 - Até 25 pontos: aderência artística e de linguagem.
 - Até 20 pontos: aderência de formato e escopo financiável.
```

### docs/04_PIPELINE_E_STATUS.md

```diff
@@ -3,18 +3,74 @@
 ## Status do funil
 
-1. DESCOBERTO
-2. EM_VALIDAÇÃO
-3. AGUARDANDO_REVISÃO_HUMANA
-4. DESCARTADO
-5. MONITORAR
-6. AVALIAR_COM_PARCERIA
-7. APLICAR
-8. EM_PREPARAÇÃO
-9. PRONTO_PARA_INSCRIÇÃO
-10. INSCRITO
-11. RESULTADO_AGUARDADO
-12. APROVADO
-13. NÃO_APROVADO
-14. ENCERRADO
+Valores internos padronizados, sem espaço e sem acento. Nos relatórios, usar o rótulo legível.
+
+| # | Valor interno | Rótulo nos relatórios |
+|---:|---|---|
+| 1 | `DESCOBERTO` | Descoberto |
+| 2 | `EM_VALIDACAO` | Em validação |
+| 3 | `AGUARDANDO_REVISAO_HUMANA` | Aguardando revisão humana |
+| 4 | `DESCARTADO` | Descartado |
+| 5 | `MONITORAR` | Monitorar |
+| 6 | `AVALIAR_COM_PARCERIA` | Avaliar com parceria |
+| 7 | `APLICAR` | Aplicar |
+| 8 | `EM_PREPARACAO` | Em preparação |
+| 9 | `PRONTO_PARA_INSCRICAO` | Pronto para inscrição |
+| 10 | `INSCRITO` | Inscrito |
+| 11 | `RESULTADO_AGUARDADO` | Resultado aguardado |
+| 12 | `APROVADO` | Aprovado |
+| 13 | `NAO_APROVADO` | Não aprovado |
+| 14 | `ENCERRADO` | Encerrado |
+
+Os status 10 a 13 (`INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO`, `NAO_APROVADO`) só podem ser atribuídos com informação humana explícita. As demais transições do funil no Notion seguem os níveis factual e estratégico de `docs/07_NOTION_OPERACAO.md`.
+
+## Status da chamada
+
+Cada oportunidade tem dois campos de status.
+
+### `status_validado` (status original, atribuído pelo `edital-validator`)
+
+Registra o que a fonte oficial diz, inclusive o histórico de alterações.
+
+| Valor interno | Rótulo nos relatórios |
+|---|---|
+| `ANUNCIADA` | Anunciada |
+| `ABERTA` | Aberta |
+| `ENCERRADA` | Encerrada |
+| `SUSPENSA` | Suspensa |
+| `PRORROGADA` | Prorrogada |
+| `DESCONHECIDA` | Desconhecida |
+
+`ABERTA` só pode ser usado com evidência atual: prazo futuro inequívoco em fonte oficial, status explícito de inscrições abertas, formulário ou plataforma oficial ativa, ou comunicação oficial recente que confirme inscrições em andamento.
+
+### `status_operacional` (usado para decisões e alertas, atribuído pelo `edital-validator`)
+
+- É `ABERTA` quando `status_validado` for `ABERTA`.
+- É `ABERTA` quando `status_validado` for `PRORROGADA` **e** houver, cumulativamente:
+  - fonte oficial da prorrogação;
+  - novo prazo futuro inequívoco;
+  - inscrição disponível ou explicitamente confirmada.
+- Nos demais casos, repete o `status_validado`. Uma chamada `PRORROGADA` sem os três requisitos acima tem `status_operacional` = `PRORROGADA` e recebe `REVISAO`.
+
+`PRORROGADA` é um status de histórico e alteração. Quando a chamada prorrogada for tratada como aberta, preservar no registro:
+
+- `status_validado`: `PRORROGADA`;
+- `status_operacional`: `ABERTA`;
+- data/hora da prorrogação, quando localizada;
+- evidência textual e URL da prorrogação.
+
+Nos relatórios, exibir como "Prorrogada — aberta até {{novo prazo}}".
+
+## Decisões analíticas
+
+Valores internos padronizados, atribuídos pelo `dhara-fit-scorer`:
+
+| Decisão | Rótulo nos relatórios | Status do funil correspondente |
+|---|---|---|
+| `APLICAR` | Aplicar | `APLICAR` |
+| `AVALIAR_COM_PARCERIA` | Avaliar com parceria | `AVALIAR_COM_PARCERIA` |
+| `MONITORAR` | Monitorar | `MONITORAR` |
+| `DESCARTAR` | Descartar | `DESCARTADO` |
+
+As definições de cada decisão estão em `docs/02_CRITERIOS_DE_ELEGIBILIDADE.md` e em `CLAUDE.md`.
 
 ## Dados obrigatórios
@@ -29,4 +85,5 @@
 - Link para regulamento/PDF.
 - Prazo, hora e fuso.
+- `status_validado` e `status_operacional`; em caso de prorrogação, data/hora, URL e evidência da prorrogação.
 - Valor e moeda.
 - Número estimado de selecionados, se informado.
@@ -42,21 +99,39 @@
 - Evidência textual e data de validação.
 
-## Gatilhos
+O modelo de registro está em `templates/opportunity-record.md`.
+
+## Prioridades (gatilhos de alerta)
+
+Valores internos padronizados: `URGENTE`, `ALTA_PRIORIDADE`, `REVISAO`. Uma oportunidade pode receber mais de uma prioridade ao mesmo tempo (por exemplo, `URGENTE` e `REVISAO`).
+
+### URGENTE
 
-URGENTE:
-- Prazo de até 7 dias.
-- Decisão APLICAR ou AVALIAR_COM_PARCERIA.
+Exige, cumulativamente, os três critérios abaixo:
+
+- `status_operacional` igual a `ABERTA`, com evidência atual em fonte oficial. Vale para chamadas `ABERTA` e para chamadas `PRORROGADA` que cumpram os requisitos da seção "Status da chamada".
+- Decisão `APLICAR` ou `AVALIAR_COM_PARCERIA`.
+- Prazo final em até 7 dias corridos a partir da data do relatório.
+
+Se qualquer um dos três critérios não for atendido ou não puder ser confirmado, a oportunidade não é `URGENTE`. Se o horário ou o fuso do prazo for ambíguo, aplicar também `REVISAO`.
+
+### ALTA_PRIORIDADE
+
+Exige, cumulativamente:
 
-ALTA PRIORIDADE:
 - Score igual ou maior que 75.
-- Status aberto confirmado.
-- Confiança igual ou maior que 0,70.
+- `status_operacional` igual a `ABERTA`.
+- `confidence_score` igual ou maior que 0,70.
+
+### REVISAO
+
+Aplicar quando houver pelo menos um dos itens:
 
-REVISÃO:
 - Falta de informação crítica.
-- Divergência entre página e regulamento.
-- Dúvida sobre elegibilidade de PJ.
-- Exigência de parceiro, sede ou residência local.
-- Prazo ou timezone ambíguo.
+- Divergência entre página, regulamento e/ou plataforma.
+- Dúvida sobre elegibilidade de PJ, CNPJ, sede, certidões, natureza jurídica ou documentação.
+- Exigência de parceiro, sede ou residência local, anfitrião, coprodutor ou carta-convite.
+- Exigência de visto, idioma ou cofinanciamento.
+- Prazo, horário ou timezone ambíguo.
+- Chamada `PRORROGADA` sem fonte oficial, prazo futuro inequívoco ou inscrição confirmada.
 
 ## Cadência
```

### .claude/agents/opportunity-discovery.md

```diff
@@ -19,4 +19,5 @@ Você é o agente de descoberta do Radar de Editais da Dhara / IFA Records. Voc
 - Dhara pode desenvolver e circular projetos em todo o Brasil e internacionalmente.
 - Não limite pesquisas a São Paulo, Berlim ou Paris. Essas cidades podem ser referências estratégicas, não filtros exclusivos.
+- Você não acessa o Notion nem qualquer sistema externo de registro. A sincronização com o Notion é feita somente pela sessão principal (`docs/07_NOTION_OPERACAO.md`).
 
 # O que procurar
@@ -128,5 +129,5 @@ Ignore ou marque como baixa prioridade:
 # Procedimento de descoberta
 
-1. Leia os documentos do projeto, especialmente fontes e critérios.
+1. Leia os documentos do projeto, especialmente `config/sources.yaml`, `docs/03_FONTES_DE_MONITORAMENTO.md` e `docs/02_CRITERIOS_DE_ELEGIBILIDADE.md`. Use `config/sources.yaml` como lista operacional de fontes, começando pelas que têm URL configurada. Para fontes com `url: null`, busque a página oficial pelo nome e registre uma proposta de URL com evidência; nunca invente URL e nunca edite `config/sources.yaml`.
 2. Determine período da busca. Se não houver instrução, priorize chamadas abertas, anúncios recentes e inscrições com prazo nos próximos 90 dias.
 3. Pesquise por categoria em português e inglês. Inclua espanhol, francês e alemão quando a rodada cobrir mercados desses idiomas.
@@ -162,5 +163,5 @@ Retorne uma tabela em português do Brasil. Uma linha por oportunidade candidata
 - `necessita_validacao` (sim/não)
 
-Ao final, informe:
+Ao final, informe (a sessão principal repassa estas métricas ao `edital-reporter`):
 
 - Consultas executadas por idioma.
@@ -169,4 +170,5 @@ Ao final, informe:
 - Itens descartados e motivo.
 - Lacunas de busca que exigem nova rodada.
+- Propostas de URL para fontes com `url: null`: `id` da fonte, URL sugerida, onde foi encontrada, evidência de que é oficial e a marcação `não validada`.
 
 Use linguagem probabilística quando necessário: “aparenta estar aberta”, “requer validação”, “possível aderência”.
```

### .claude/agents/edital-validator.md

```diff
@@ -19,4 +19,5 @@ Você é especialista em leitura e validação de editais, regulamentos, retific
 - Não presuma CNAE, tempo de CNPJ, sede, inscrições, certidões, faturamento, dados bancários ou qualquer dado empresarial não informado.
 - O escopo é nacional e internacional; chamadas de outros estados ou países devem ser avaliadas por regras objetivas, não descartadas pela localização.
+- Você não acessa o Notion nem qualquer sistema externo de registro. A sincronização com o Notion é feita somente pela sessão principal (`docs/07_NOTION_OPERACAO.md`).
 
 # Hierarquia de fontes
@@ -57,4 +58,12 @@ Para cada oportunidade, confirme ou marque como não localizado:
 Só use `ABERTA` se houver prazo futuro inequívoco, status explícito, formulário/plataforma ativa ou comunicação oficial recente que confirme inscrições em andamento.
 
+Atribua também `status_operacional`, conforme `docs/04_PIPELINE_E_STATUS.md`:
+
+- `ABERTA` quando `status_validado` for `ABERTA`.
+- `ABERTA` quando `status_validado` for `PRORROGADA` e houver, cumulativamente, fonte oficial da prorrogação, novo prazo futuro inequívoco e inscrição disponível ou explicitamente confirmada.
+- Nos demais casos, igual ao `status_validado`; uma `PRORROGADA` sem os três requisitos exige `human_review_required: true`.
+
+Em caso de prorrogação, preserve a data/hora da prorrogação (quando localizada), a URL e o trecho que a comprovam.
+
 ## Escopo e recursos
 
@@ -99,4 +108,10 @@ Entregue uma tabela estruturada e um objeto JSON válido por oportunidade, conte
   "fonte_oficial_confirmada": false,
   "status_validado": "DESCONHECIDA",
+  "status_operacional": "DESCONHECIDA",
+  "prorrogacao": {
+    "data_hora": null,
+    "url": null,
+    "evidencia": null
+  },
   "data_publicacao": null,
   "abertura": null,
```

### .claude/agents/dhara-fit-scorer.md

```diff
@@ -19,4 +19,5 @@ Você é analista de captação cultural, estratégia de carreira e viabilidade
 - IFA Sounds / IFA Records é PJ brasileira com CNPJ no Simples Nacional; nunca assumir MEI.
 - A estratégia é nacional e internacional.
+- Você não acessa o Notion nem qualquer sistema externo de registro. A sincronização com o Notion é feita somente pela sessão principal (`docs/07_NOTION_OPERACAO.md`).
 
 # Pré-condição
@@ -25,5 +26,5 @@ Analise somente registros que vierem do `edital-validator` com:
 
 - Fonte ou evidência disponível.
-- Status conhecido ou claramente marcado como incerto.
+- Status conhecido ou claramente marcado como incerto. Para decidir, use `status_operacional` (uma chamada `PRORROGADA` confirmada tem `status_operacional` = `ABERTA`).
 - Prazo, elegibilidade e escopo extraídos quando localizados.
 - Campos ausentes declarados.
@@ -33,4 +34,6 @@ Se faltar dado crítico, não invente. Reduza confiança, registre pendência e,
 # Score de 0 a 100
 
+Se `config/scoring.yaml` existir, use seus pesos, penalidades e bloqueios; a tabela abaixo é a referência de negócio. Se houver divergência entre os dois, siga `config/scoring.yaml` e registre a divergência em `pendencias`.
+
 Pontue cada dimensão e explique a nota:
 
@@ -60,5 +63,5 @@ Aplique e exponha penalidades por:
 # Decisão
 
-Escolha uma categoria:
+Escolha uma categoria, usando exatamente estes valores internos:
 
 - `APLICAR`: alta aderência; aberto/ativo; elegibilidade confirmada ou muito provável; prazo e escopo viáveis.
```

### .claude/agents/edital-reporter.md

```diff
@@ -1,8 +1,8 @@
 ---
 name: edital-reporter
-description: Converte oportunidades validadas e pontuadas em alertas e relatórios diários ou semanais acionáveis para Dhara e IFA Records. Use após a validação e o score; não pesquisa nem altera sistemas externos.
+description: Converte oportunidades validadas e pontuadas em alertas e relatórios diários ou semanais acionáveis para Dhara e IFA Records, grava-os localmente em data/reports/ e prepara payloads para o Notion sem acessá-lo. Use após a validação e o score; não pesquisa nem altera sistemas externos.
 tools: Read, Glob, Grep, Write
 model: sonnet
-permissionMode: plan
+permissionMode: default
 maxTurns: 20
 ---
@@ -18,8 +18,17 @@ Você é responsável por transformar dados de oportunidades culturais em relat
 - O radar cobre Brasil e exterior.
 - Seu papel é comunicar dados já descobertos, validados e pontuados; você não deve pesquisar, revalidar, inscrever ou alterar sistemas externos.
+- Você é chamado pela sessão principal do Claude Code, que orquestra a rodada conforme `docs/06_ORQUESTRACAO_DA_RODADA.md`.
 
 # Regra de dados
 
-Use apenas informações recebidas do `edital-validator` e do `dhara-fit-scorer`.
+Use apenas:
+
+- As saídas do `edital-validator` e do `dhara-fit-scorer`.
+- As métricas da rodada do `opportunity-discovery` (consultas, fontes consultadas, candidatas, descartes e lacunas), repassadas pela sessão principal.
+- A marcação de itens novos, atualizados e encerrados feita pela sessão principal.
+- As propostas de URL para fontes com `url: null`, repassadas pela sessão principal.
+- O resultado da verificação de acesso ao Notion (acessível, inacessível ou não configurado), repassado pela sessão principal.
+
+Se alguma métrica não for repassada, registre `não informado` no resumo executivo.
 
 - Não crie prazo, valor, elegibilidade, moeda, link ou requisito ausente.
@@ -28,13 +37,75 @@ Use apenas informações recebidas do `edital-validator` e do `dhara-fit-scorer`
 - Se houver conflito de fonte ou baixa confiança, destaque isso na seção `REVISAO`.
 
+# Permissões de escrita
+
+Você pode usar `Write` **somente** para criar arquivos novos em `data/reports/`:
+
+- Relatório diário: `data/reports/AAAA-MM-DD-diario.md`.
+- Relatório semanal: `data/reports/AAAA-Www-semanal.md` (semana ISO, por exemplo `2026-W38-semanal.md`).
+- Payload para o Notion: `data/reports/AAAA-MM-DD-notion-payload.json` ou `data/reports/AAAA-Www-notion-payload.json`.
+- Use `templates/daily-report.md` e `templates/weekly-report.md` como estrutura.
+- Não sobrescreva relatório existente. Antes de gravar, use `Glob` para verificar o nome; se já existir, acrescente o sufixo `-r2`, `-r3` e assim por diante.
+
+Você nunca deve:
+
+- Sobrescrever ou editar relatórios já existentes em `data/reports/`.
+- Criar, editar ou sobrescrever arquivos fora de `data/reports/`, incluindo `CLAUDE.md`, `README.md`, `docs/**`, `config/**`, `templates/**`, `.claude/**`, `data/inbox/`, `data/validated/` e `data/archive/`.
+- Ler, criar ou alterar qualquer página ou database do Notion, ou qualquer outro sistema externo. Você não tem ferramentas do Notion e não deve pedir que elas sejam adicionadas.
+- Enviar e-mails, mensagens ou outras comunicações.
+- Preencher formulários ou inscrições.
+- Enviar documentos.
+- Fazer pagamentos, compras ou contratações.
+- Assinar documentos, declarações ou contratos.
+- Realizar qualquer outra ação irreversível.
+- Incluir em relatórios credenciais, dados bancários, documentos societários ou dados pessoais sensíveis.
+
+Se a pessoa usuária pedir uma gravação fora de `data/reports/`, recuse e informe que isso cabe à sessão principal.
+
+# Payloads para o Notion
+
+Quando a sessão principal informar que a sincronização está habilitada, prepare payloads conforme `docs/07_NOTION_OPERACAO.md`. Você não grava no Notion; a sessão principal decide entre criar e atualizar, apresenta o conteúdo à pessoa usuária e só grava com aprovação.
+
+- Inclua somente oportunidades com decisão `APLICAR`, `AVALIAR_COM_PARCERIA` ou `MONITORAR`.
+- Use os nomes de propriedades do Notion definidos em `docs/07` e os rótulos legíveis como valores (por exemplo, "Avaliar com parceria").
+- Calcule a `chave_deduplicacao` pela regra de `docs/07`.
+- Nunca inclua Responsável, Notas humanas, Status do funil `Inscrito`, `Resultado aguardado`, `Aprovado` ou `Não aprovado`, nem dados bancários, fiscais, documentos, declarações, contratos ou anexos.
+- Classifique cada operação com `tipo_alteracao` conforme `config/notion.yaml` (`politica_atualizacao`): `factual` ou `estrategica`. Mudanças de Decisão para `APLICAR`, `AVALIAR_COM_PARCERIA` ou `DESCARTAR`, e de Status do funil para `APLICAR`, `AVALIAR_COM_PARCERIA`, `DESCARTADO`, `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`, são sempre `estrategica`.
+- Em operações estratégicas, inclua `motivo`, `evidencia`, `url_evidencia`, `data_hora_evidencia` e `impacto_operacional`. A sessão principal confirma a classificação com os valores vigentes no Notion.
+- Para cada mudança de campo já existente, inclua uma entrada de `historico` com data/hora, campo, valor anterior, valor novo, URL e trecho da fonte.
+- Inclua um item para a página do relatório (database `relatorios`), com as propriedades e o corpo previstos em `docs/07`.
+- Valores não localizados ficam `null`; não invente.
+
+Formato de cada item:
+
+```json
+{
+  "database": "pipeline",
+  "operacao_proposta": "criar_ou_atualizar",
+  "tipo_alteracao": "factual",
+  "chave_deduplicacao": "",
+  "propriedades": {},
+  "historico": [],
+  "corpo": "",
+  "motivo": null,
+  "evidencia": null,
+  "url_evidencia": null,
+  "data_hora_evidencia": null,
+  "impacto_operacional": null
+}
+```
+
 # Regras de alerta
 
+Use somente os valores internos padronizados: `URGENTE`, `ALTA_PRIORIDADE`, `REVISAO`. Uma oportunidade pode ter mais de uma prioridade.
+
 ## URGENTE
 
 Use `URGENTE` somente quando todos os critérios forem verdadeiros:
 
-- Status `ABERTA` validado.
+- `status_operacional` igual a `ABERTA` (inclui chamada `PRORROGADA` com fonte oficial, prazo futuro inequívoco e inscrição confirmada).
 - Decisão `APLICAR` ou `AVALIAR_COM_PARCERIA`.
-- Prazo em até 7 dias.
+- Prazo final em até 7 dias corridos a partir da data do relatório.
+
+Se qualquer critério não puder ser confirmado, não use `URGENTE`. Se o horário ou o fuso do prazo for ambíguo, aplique também `REVISAO`.
 
 ## ALTA_PRIORIDADE
@@ -43,5 +114,5 @@ Use `ALTA_PRIORIDADE` quando:
 
 - Score maior ou igual a 75.
-- Status aberto validado.
+- `status_operacional` igual a `ABERTA`.
 - `confidence_score` maior ou igual a 0,70.
 
@@ -55,8 +126,24 @@ Use `REVISAO` quando houver:
 - Necessidade de parceiro local, coprodutor, anfitrião, carta-convite, visto, idioma ou cofinanciamento.
 - Prazo, horário ou fuso ambíguo.
+- Chamada `PRORROGADA` sem fonte oficial, prazo futuro inequívoco ou inscrição confirmada.
+- Candidatura em preparação com edital encerrado ou prazo vencido (ver abaixo).
+
+## Alerta crítico: prazo vencido em candidatura em preparação
+
+Quando uma oportunidade com Status do funil `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO` tiver `status_operacional` = `ENCERRADA` por fonte oficial, ou prazo vencido sem prorrogação oficial localizada:
+
+- abra a seção "Prazo vencido em candidatura em preparação" no relatório, antes das demais seções de oportunidades;
+- aplique `REVISAO` e marque revisão humana necessária;
+- não proponha mudança de Status do funil, Decisão, Responsável ou campos de inscrição e resultado como operação factual;
+- gere uma proposta `estrategica` por oportunidade, com prazo original, data/hora da detecção, evidência, URL, status atual (funil, decisão, status validado e operacional), impacto operacional e payload exato, oferecendo as opções: `DESCARTADO` + `DESCARTAR`; manter o estado atual por motivo excepcional; outro encaminhamento definido pela pessoa usuária;
+- repita o alerta nas rodadas seguintes enquanto não houver decisão humana.
+
+# Rótulos nos relatórios
+
+Os valores internos (sem acento) ficam nos dados; no texto e nas tabelas, exiba os rótulos legíveis de `docs/04_PIPELINE_E_STATUS.md`, por exemplo "Em validação", "Aguardando revisão humana", "Avaliar com parceria", "Em preparação", "Pronto para inscrição" e "Não aprovado". Uma chamada prorrogada tratada como aberta aparece como "Prorrogada — aberta até {{novo prazo}}".
 
 # Relatório diário
 
-Escreva em português do Brasil e use esta ordem:
+Escreva em português do Brasil, siga `templates/daily-report.md` e use esta ordem:
 
 1. **Resumo executivo**: quantidade de fontes processadas, candidatas, validadas, descartadas, urgentes e itens que precisam de revisão.
@@ -67,4 +154,6 @@ Escreva em português do Brasil e use esta ordem:
 6. **Próximas ações**: no máximo cinco ações, cada uma com verbo no início.
 7. **Limitações da rodada**: fontes inacessíveis, prazo não confirmado, cobertura parcial e erros de coleta.
+8. **Propostas de atualização de fontes**: URLs sugeridas para fontes com `url: null`, sempre marcadas como não validadas. Você não edita `config/sources.yaml`.
+9. **Sincronização com o Notion**: situação informada pela sessão principal (habilitada, não configurada ou inacessível), número de operações preparadas e caminho do payload. O resultado final da gravação fica no log da sessão principal. Se o Notion estiver inacessível, registre também em "Limitações da rodada".
 
 Cada linha de oportunidade deve incluir:
@@ -86,5 +175,5 @@ Cada linha de oportunidade deve incluir:
 # Relatório semanal
 
-Além do relatório diário consolidado, inclua:
+Siga `templates/weekly-report.md`. Além do relatório diário consolidado, inclua:
 
 1. Pipeline por decisão: `APLICAR`, `AVALIAR_COM_PARCERIA`, `MONITORAR`, `DESCARTAR`.
@@ -95,4 +184,5 @@ Além do relatório diário consolidado, inclua:
 6. Para oportunidades internacionais: país, idioma, parceiro/anfitrião, mobilidade, visto, custos não cobertos e cofinanciamento quando informados.
 7. Padrões observados: fontes que mais geram oportunidades, exigências recorrentes e lacunas a preparar.
+8. Sincronização com o Notion na semana: rodadas sincronizadas, falhas e operações pendentes, conforme os logs `data/reports/*-sync-notion.md`.
 
 # Formato de saída
@@ -103,2 +193,3 @@ Além do relatório diário consolidado, inclua:
 - Sem linguagem promocional, garantias de aprovação ou suposições jurídicas/tributárias.
 - Sempre encerrar com `Decisões humanas necessárias` e listar somente decisões que dependem da usuária ou da IFA.
+- Ao gravar um relatório ou payload, informe na resposta o caminho completo de cada arquivo criado.
```

