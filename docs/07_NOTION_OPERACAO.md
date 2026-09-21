# Notion como camada operacional

Este documento define como o Radar de Editais — Dhara / IFA Records usa o Notion.

## Papéis

| Camada | Papel |
|---|---|
| Repositório (GitHub) | Fonte de verdade das regras, agentes, critérios, fontes, templates e configurações. |
| Notion | Sistema de registro operacional: pipeline de oportunidades, relatórios diários e semanais, histórico de alterações. |
| Sessão principal do Claude Code | Orquestradora e **única** responsável por ler e gravar no Notion. |
| Subagentes | Nunca acessam o Notion. O `edital-reporter` pode apenas preparar payloads. |

Nenhum subagente recebe ferramentas do Notion. O campo `tools` de cada arquivo em `.claude/agents/` lista as ferramentas permitidas e não inclui ferramentas MCP; não adicione ferramentas do Notion a esses arquivos.

## Conector e permissões

### Conector

- Servidor MCP oficial do Notion: `https://mcp.notion.com/mcp` (transporte HTTP, autenticação OAuth).
- No Claude Code, o servidor é adicionado com `claude mcp add --transport http notion https://mcp.notion.com/mcp` e autenticado com `/mcp`. A conexão feita no claude.ai não é herdada pelo Claude Code; cada ambiente tem a sua.
- Os nomes completos das ferramentas no Claude Code seguem o padrão `mcp__<nome-do-servidor>__<ferramenta>`, por exemplo `mcp__notion__notion-fetch` quando o servidor se chama `notion`. Confirme os nomes com `/mcp` após a conexão.

### Acesso no Notion

- O servidor MCP age com as permissões da conta que fez o OAuth. Essa conta precisa de acesso de edição às duas databases e à página onde elas ficam.
- Não é necessário acesso de administrador do workspace.
- Recomendação: manter as duas databases dentro de uma única página dedicada, por exemplo "Radar de Editais — IFA Records", para limitar o alcance das buscas.

### Ferramentas usadas

| Ferramenta | Uso | Quando |
|---|---|---|
| `notion-get-tool-access` | Verificar ferramentas e restrições disponíveis na conexão | Primeira conexão e quando uma ferramenta falhar |
| `notion-search` ou `notion-ai-search` | Localizar as duas databases pelo nome | Primeira conexão |
| `notion-fetch` | Ler database, schema (data source) e páginas existentes | Toda rodada, antes de qualquer escrita |
| `notion-query-data-sources` | Buscar registro existente pela chave de deduplicação | Toda sincronização |
| `notion-create-pages` | Criar oportunidade ou relatório | Somente após aprovação |
| `notion-update-page` com `update_properties` | Atualizar propriedades permitidas | Factual: após o resumo em lote; estratégica: após aprovação da prévia |
| `notion-update-page` com `insert_content` (posição `end`) | Acrescentar entrada ao histórico da página | Somente após aprovação |
| `notion-create-database` | Criar as databases de produção ou de teste | Somente na configuração inicial, com aprovação explícita |

### Ferramentas e comandos proibidos na operação

- `notion-update-data-source` (altera schema, título ou envia a database para a lixeira). Mudanças de schema são feitas por pessoa humana ou em sessão de configuração aprovada.
- `notion-update-page` com `replace_content` ou `update_content`, e qualquer uso de `allow_deleting_content`.
- `notion-move-pages`, `notion-duplicate-page`, `notion-create-comment`, `notion-create-view`, `notion-update-view`.
- Qualquer operação que apague, arquive ou envie páginas para a lixeira.
- `notion-create-file-upload` e qualquer anexo de arquivo a páginas.
- Ferramentas de agentes, sessões ou skills do Notion.

As permissões locais em `.claude/settings.json` protegem apenas arquivos locais e **não** controlam o Notion. Não pré-aprove as ferramentas de escrita do Notion (`notion-create-pages`, `notion-update-page`) com "não perguntar novamente"; a confirmação a cada escrita faz parte desta política.

## Configuração local

Os identificadores resolvidos ficam em `config/notion.yaml`. Eles não são segredos, mas o arquivo só é alterado por pessoa humana ou com aprovação explícita. Enquanto os IDs estiverem `null`, nenhuma escrita no Notion é permitida.

## Database 1: `Pipeline de Editais — IFA Records`

Uma página por oportunidade. Propriedades guardam o **valor atual**; o corpo da página guarda o **histórico** e as evidências.

### Propriedades

Evite propriedades chamadas "ID" ou "URL": o conector exige tratamento especial para esses nomes.

| Propriedade | Tipo | Valores permitidos | Quem altera |
|---|---|---|---|
| Oportunidade | Title | Título oficial | Radar |
| Chave de deduplicação | Text | Ver "Chave de deduplicação" | Radar, só na criação |
| Identificador externo | Text | Número/código oficial da chamada | Radar |
| Instituição | Text | — | Radar |
| Tipo | Select | Edital, Prêmio, Residência, Festival, Showcase, Contratação, Intercâmbio, Outro | Radar |
| Linguagem | Multi-select | Música, Produção fonográfica, Audiovisual musical, Artes integradas, Cultura digital, Formação de público, Outro | Radar |
| Modalidade | Text | — | Radar |
| País | Text | — | Radar |
| Estado/região | Text | — | Radar |
| Cidade | Text | — | Radar |
| Abrangência | Select | Municipal, Estadual, Nacional, Internacional | Radar |
| Cobertura | Select | Brasil, Internacional | Radar |
| Status do funil | Select | Rótulos de `docs/04`: Descoberto, Em validação, Aguardando revisão humana, Descartado, Monitorar, Avaliar com parceria, Aplicar, Em preparação, Pronto para inscrição, Inscrito, Resultado aguardado, Aprovado, Não aprovado, Encerrado | Ver "Campo do Notion → política de atualização" |
| Status validado | Select | Anunciada, Aberta, Encerrada, Suspensa, Prorrogada, Desconhecida | Radar |
| Status operacional | Select | Anunciada, Aberta, Encerrada, Suspensa, Prorrogada, Desconhecida | Radar |
| Decisão | Select | Aplicar, Avaliar com parceria, Monitorar, Descartar | Ver "Campo do Notion → política de atualização" |
| Decisão proposta | Select | Aplicar, Avaliar com parceria, Monitorar, Descartar | Radar, somente em modo agendado |
| Proposta estratégica | Text | Valor atual, valor proposto, motivo, evidência, URL e data/hora | Radar, somente em modo agendado |
| Prioridade | Multi-select | Urgente, Alta prioridade, Revisão | Radar |
| Revisão humana necessária | Checkbox | — | Radar |
| Prazo final | Date (com hora) | — | Radar |
| Fuso do prazo | Text | Como informado pela fonte | Radar |
| Prazo original (texto) | Text | Trecho literal da fonte | Radar |
| Data da prorrogação | Date (com hora) | — | Radar |
| Abertura | Date (com hora) | — | Radar |
| Valor máximo | Number | — | Radar |
| Moeda | Select | BRL, EUR, USD, GBP, Outra | Radar |
| PJ aceita | Select | Sim, Não, Não localizado | Radar |
| Exige parceiro local | Select | Sim, Não, Não localizado | Radar |
| Fonte oficial confirmada | Checkbox | — | Radar |
| Score | Number | 0 a 100 | Radar |
| Confiança | Number (percentual) | 0 a 1 | Radar |
| Motivo principal | Text | — | Radar |
| Maior risco | Text | — | Radar |
| Pendências | Text | — | Radar |
| Próxima ação | Text | — | Radar |
| Link oficial | URL | — | Radar |
| Link de inscrição | URL | — | Radar |
| Regulamento | URL | — | Radar |
| Link de descoberta | URL | — | Radar |
| Fonte de descoberta | Select | Oficial, PROSAS, Parceiro, Mídia, Newsletter, Rede social | Radar |
| Última validação | Date (com hora) | — | Radar |
| Relatórios | Relation (duas vias) → Relatórios do Radar | — | Radar (acrescenta, nunca remove) |
| Responsável | People | — | **Somente humano** |
| Notas humanas | Text | — | **Somente humano** |

### Corpo da página

```markdown
## Resumo
## Evidências
## Histórico de alterações
## Checklist inicial
```

- **Evidências**: tabela com afirmação, trecho curto da fonte, URL e data/hora da coleta, gravada na criação.
- **Histórico de alterações**: somente acréscimos, com `insert_content` no fim da página. Cada entrada registra data/hora, campo, valor anterior, valor novo, fonte (URL) e trecho. Entradas anteriores nunca são editadas ou removidas.

## Database 2: `Relatórios do Radar — IFA Records`

Uma página por relatório. Páginas não são editadas depois de criadas.

| Propriedade | Tipo | Valores permitidos | Quem altera |
|---|---|---|---|
| Relatório | Title | "Diário AAAA-MM-DD" ou "Semanal AAAA-Www", com sufixo "r2", "r3" se necessário | Radar, na criação |
| Chave do relatório | Text | `diario:AAAA-MM-DD` ou `semanal:AAAA-Www`, com `-r2`, `-r3` | Radar, na criação |
| Tipo | Select | Diário, Semanal | Radar, na criação |
| Data/hora da rodada | Date (com hora) | — | Radar, na criação |
| Cobertura | Select | Brasil, Internacional, Brasil e internacional | Radar, na criação |
| Modo de execução | Select | Subagentes formais, Modo agente único | Radar, na criação |
| Fontes consultadas | Number | — | Radar, na criação |
| Candidatas | Number | — | Radar, na criação |
| Validadas | Number | — | Radar, na criação |
| Descartadas | Number | — | Radar, na criação |
| Urgentes | Number | — | Radar, na criação |
| Em revisão | Number | — | Radar, na criação |
| Alta prioridade | Number | — | Radar, na criação |
| Propostas de URL | Number | — | Radar, na criação |
| Sincronização do pipeline | Select | Concluída, Parcial, Falhou, Não realizada | Radar, na criação |
| Oportunidades | Relation (duas vias) → Pipeline de Editais | — | Radar, na criação |
| Arquivo local | Text | Caminho em `data/reports/` | Radar, na criação |
| Decisões humanas pendentes | Checkbox | — | Radar na criação; depois, humano |

### Corpo da página

Na ordem: tipo; data/hora da rodada; cobertura; fontes consultadas; números de candidatas, validadas, descartadas, urgentes e em revisão; oportunidades urgentes; novas oportunidades prioritárias; mudanças de prazo, regulamento, status, valor ou elegibilidade; propostas de novas URLs para `config/sources.yaml` (não validadas, sem edição automática do arquivo); limitações da rodada, incluindo falhas de sincronização; próximas ações; decisões humanas necessárias.

## Relação entre as databases

- `Pipeline.Relatórios` ↔ `Relatórios.Oportunidades` (relação de duas vias).
- Ao criar um relatório, a relação aponta para as oportunidades criadas ou atualizadas na rodada.
- A relação só recebe acréscimos; o radar nunca remove vínculos.

## Política de escrita

### Pré-condições

A sessão principal só grava uma oportunidade depois de, nesta ordem:

1. Descoberta (`opportunity-discovery`).
2. Validação em fonte oficial, ou registro explícito de que a fonte oficial não foi localizada (`edital-validator`).
3. Análise de elegibilidade e score (`dhara-fit-scorer`).
4. Classificação final com decisão.

E somente se:

- `config/notion.yaml` tiver os IDs resolvidos e `schema_verificado: true`;
- o schema lido na rodada (`notion-fetch`) coincidir com este documento;
- a decisão for `APLICAR`, `AVALIAR_COM_PARCERIA` ou `MONITORAR`.

Oportunidades com decisão `DESCARTAR` não são criadas. Uma oportunidade já registrada só passa a `DESCARTAR` pelo fluxo de atualização estratégica.

### Níveis de atualização

Toda escrita no Notion pertence a um de três níveis. A regra completa por campo está em `config/notion.yaml` (`politica_atualizacao`) e na tabela "Campo do Notion → política de atualização".

| Nível | O que é | Como é confirmado |
|---|---|---|
| **Factual** | Mudança objetiva, derivada de fonte validada ou de regra do radar | Apresentada em lote no resumo da sincronização e confirmada na permissão da ferramenta, sem prévia estratégica |
| **Estratégica** | Mudança de rumo da candidatura | Prévia completa por oportunidade e aprovação explícita da pessoa usuária antes de gravar |
| **Exclusivamente humana** | Estados de inscrição e resultado, responsáveis, notas e dados sensíveis | O radar nunca grava; no máximo lembra em "Decisões humanas necessárias" |

"Automático" neste documento significa **sem a prévia estratégica**. Não significa gravar sem confirmação: as ferramentas `notion-create-pages` e `notion-update-page` nunca são pré-aprovadas, então toda gravação passa pela permissão da ferramenta no Claude Code, exceto no modo agendado (ver seção própria).

### Atualização factual

Permitida quando houver evidência validada na rodada:

- Prazo final, Fuso do prazo e Prazo original (texto).
- Abertura e Data da prorrogação.
- Status validado e Status operacional.
- Valor máximo, Moeda, Link oficial, Link de inscrição, Regulamento, Link de descoberta e Fonte de descoberta.
- Fonte oficial confirmada.
- Score e Confiança.
- Prioridade e Revisão humana necessária.
- Motivo principal, Maior risco e Pendências.
- Próxima ação e Última validação.
- Relação Relatórios (somente acréscimo).
- Evidências e Histórico de alterações, somente por acréscimo no corpo da página.
- Status do funil para `EM_VALIDACAO`, `AGUARDANDO_REVISAO_HUMANA`, `ENCERRADO` ou `MONITORAR`, somente pelos gatilhos objetivos abaixo.
- Decisão para `MONITORAR`, somente junto com a mudança do Status do funil para `MONITORAR` pelo mesmo gatilho, para que os dois campos não fiquem contraditórios.

Toda atualização de campo com valor anterior preenchido gera uma entrada no Histórico de alterações, na mesma operação.

#### Gatilhos objetivos do Status do funil

| Novo status | Gatilho objetivo |
|---|---|
| `EM_VALIDACAO` | Fonte oficial publicou retificação, errata, anexo ou novo regulamento que exige revalidação; ou um link oficial registrado deixou de responder |
| `AGUARDANDO_REVISAO_HUMANA` | A oportunidade recebeu `REVISAO` por dado crítico ausente, conflito de fontes, dúvida de elegibilidade ou possível duplicata |
| `ENCERRADO` | `status_operacional` = `ENCERRADA` com fonte oficial, ou prazo final vencido sem prorrogação oficial localizada |
| `MONITORAR` | `status_operacional` = `ANUNCIADA` ou `SUSPENSA` com fonte oficial |

#### Bloqueios da atualização factual do funil

- Se o Status do funil atual for `INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO` ou `NAO_APROVADO`, o radar não altera Status do funil nem Decisão em nenhuma hipótese.
- Se o Status do funil atual for `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`, qualquer mudança de Status do funil ou Decisão, inclusive por gatilho objetivo, segue o fluxo estratégico. Essas fases foram aprovadas por pessoa humana e não são desfeitas sem aprovação.
- Sem gatilho objetivo documentado, a mudança não é factual: vira proposta estratégica ou item de revisão.

### Prazo vencido em candidatura em preparação

Regra específica para registros cujo Status do funil seja `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`, quando houver fonte oficial confirmando `ENCERRADA` ou o prazo vencer sem prorrogação oficial localizada.

**Atualização factual imediata**, na mesma rodada:

- `Status validado`, quando houver confirmação oficial;
- `Status operacional` para `ENCERRADA`;
- `Prioridade` recebe `REVISAO`;
- `Revisão humana necessária` fica marcada;
- `Última validação`;
- Evidências e Histórico de alterações, por acréscimo no corpo da página.

**Nunca alterado automaticamente nesse caso:**

- Status do funil;
- Decisão;
- Responsável;
- campos de inscrição ou resultado (`INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO`, `NAO_APROVADO`).

**Alerta e proposta.** O `edital-reporter` gera um alerta crítico, em seção própria do relatório, e uma proposta estratégica por oportunidade, com as opções:

1. `DESCARTADO` + `DESCARTAR`, na mesma mudança;
2. manter o estado atual por motivo excepcional, por exemplo inscrição já protocolada fora do sistema ou prorrogação ainda não publicada;
3. outro encaminhamento definido pela pessoa usuária.

A proposta contém: prazo original, data/hora da detecção, evidência, URL, status atual (funil, decisão, status validado e operacional), impacto operacional e payload exato. Enquanto não houver resposta, o registro permanece em `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO` com `REVISAO`, e a proposta volta na rodada seguinte.

### Atualização estratégica

A sessão principal propõe, mas só grava depois de aprovação explícita da pessoa usuária, quando houver mudança de:

- Decisão para `APLICAR`, `AVALIAR_COM_PARCERIA` ou `DESCARTAR`;
- Status do funil para `APLICAR`, `AVALIAR_COM_PARCERIA`, `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`;
- Status do funil para `DESCARTADO`, que acompanha a Decisão `DESCARTAR` na mesma proposta;
- qualquer mudança de Status do funil ou Decisão quando o funil estiver em `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`, inclusive o encerramento do edital (ver "Prazo vencido em candidatura em preparação");
- troca da Chave de deduplicação (por exemplo, de `descoberta:` para a URL oficial).

A criação de uma oportunidade com Decisão `APLICAR` ou `AVALIAR_COM_PARCERIA` também usa a prévia estratégica. A criação com Decisão `MONITORAR` segue o nível factual.

### Campos exclusivamente humanos

O radar nunca grava, nem propõe gravar em payload:

- Status do funil `INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO` ou `NAO_APROVADO`;
- Responsável;
- Notas humanas;
- dados bancários, dados fiscais, documentos, declarações, contratos e anexos sensíveis, em qualquer propriedade ou no corpo da página.

O radar também não usa `notion-create-file-upload` nem anexa arquivos a páginas.

### Campos fixos após a criação

- Oportunidade (título), Identificador externo, Instituição, Tipo, Linguagem, Modalidade, País, Estado/região, Cidade, Abrangência e Cobertura são gravados na criação. Correções posteriores entram como proposta estratégica.
- Entradas anteriores do Histórico de alterações e da seção Evidências nunca são alteradas.
- Páginas da database de Relatórios nunca são alteradas depois de criadas.

### Chave de deduplicação

Ordem de preferência:

1. **URL canônica da página oficial** (`url_oficial`; se ausente, `url_regulamento`; se ausente, `url_inscricao`), normalizada: `https`, domínio em minúsculas, sem `www.`, sem fragmento (`#...`), sem parâmetros de rastreamento (`utm_*`, `fbclid`, `gclid`) e sem barra final.
2. Sem URL oficial: `id:<slug-da-instituicao>:<identificador-externo>`.
3. Sem fonte oficial localizada: `descoberta:<url_descoberta normalizada>`.

Antes de criar, a sessão principal consulta a database com `notion-query-data-sources`:

- pela Chave de deduplicação;
- pelo Link oficial;
- pelo par Instituição + Identificador externo, quando houver.

| Resultado da consulta | Ação |
|---|---|
| Nenhuma página encontrada | Propor criação |
| Exatamente uma página | Propor atualização dos campos permitidos |
| Mais de uma página | Não gravar; marcar `REVISAO` e listar as páginas para decisão humana |

O radar nunca cria duplicatas e nunca apaga páginas.

## Campo do Notion → política de atualização

| Propriedade | Na criação | Depois da criação |
|---|---|---|
| Oportunidade | Radar | Fixo; correção é estratégica |
| Chave de deduplicação | Radar | Estratégica |
| Identificador externo, Instituição, Tipo, Linguagem, Modalidade | Radar | Fixo; correção é estratégica |
| País, Estado/região, Cidade, Abrangência, Cobertura | Radar | Fixo; correção é estratégica |
| Status do funil → `EM_VALIDACAO`, `AGUARDANDO_REVISAO_HUMANA`, `ENCERRADO`, `MONITORAR` | Radar | Factual, por gatilho objetivo e fora dos bloqueios |
| Status do funil → `APLICAR`, `AVALIAR_COM_PARCERIA`, `DESCARTADO`, `EM_PREPARACAO`, `PRONTO_PARA_INSCRICAO` | Estratégica para `APLICAR` e `AVALIAR_COM_PARCERIA` | Estratégica |
| Status do funil → `INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO`, `NAO_APROVADO` | Nunca | Exclusivamente humano |
| Status do funil e Decisão com o funil em `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO` e edital encerrado ou prazo vencido | — | Estratégica, com alerta crítico; os campos factuais de status, prioridade, revisão e histórico são atualizados na hora |
| Status do funil `DESCOBERTO` | Não usado no Notion | Não usado no Notion |
| Decisão → `MONITORAR` | Factual | Factual, só junto com o funil para `MONITORAR` |
| Decisão → `APLICAR`, `AVALIAR_COM_PARCERIA` | Estratégica | Estratégica |
| Decisão → `DESCARTAR` | Não se cria | Estratégica |
| Decisão proposta | Nunca na criação interativa; radar somente em modo agendado | Radar em modo agendado; limpeza após aprovação ou recusa |
| Proposta estratégica | Nunca na criação interativa; radar somente em modo agendado | Radar em modo agendado; limpeza após aprovação ou recusa |
| Status validado, Status operacional | Radar | Factual |
| Prioridade, Revisão humana necessária | Radar | Factual |
| Prazo final, Fuso do prazo, Prazo original (texto) | Radar | Factual |
| Abertura, Data da prorrogação | Radar | Factual |
| Valor máximo, Moeda | Radar | Factual |
| Link oficial, Link de inscrição, Regulamento, Link de descoberta, Fonte de descoberta | Radar | Factual |
| Fonte oficial confirmada | Radar | Factual |
| Score, Confiança | Radar | Factual |
| Motivo principal, Maior risco, Pendências, Próxima ação | Radar | Factual |
| Última validação | Radar | Factual |
| Relatórios (relação) | Radar | Factual, somente acréscimo |
| Corpo: Evidências e Histórico de alterações | Radar | Factual, somente acréscimo com `insert_content` |
| Responsável | Nunca | Exclusivamente humano |
| Notas humanas | Nunca | Exclusivamente humano |
| Anexos, dados bancários ou fiscais, documentos, declarações, contratos | Nunca | Exclusivamente humano |
| Database de Relatórios, todas as propriedades | Radar | Nunca alteradas |

## Confirmação antes de gravar

Em toda sincronização, a sessão principal:

1. Resolve as databases e os campos com `notion-fetch` e compara com este documento.
2. Faz as consultas de deduplicação.
3. Classifica cada operação como factual, estratégica ou bloqueada (exclusivamente humana ou fora das regras). Operações bloqueadas não são enviadas; aparecem em "Decisões humanas necessárias".
4. Apresenta o **resumo factual** em lote: página, campo, valor anterior, valor novo, fonte e entrada de histórico.
5. Apresenta cada **proposta estratégica** separadamente, pelo fluxo abaixo, e aguarda a resposta para cada uma.
6. Grava as operações factuais e as estratégicas aprovadas. Cada gravação passa pela permissão da ferramenta, que nunca é pré-aprovada.
7. Lê de volta as páginas gravadas (`notion-fetch`) e confere os valores.
8. Cria por último a página do relatório.
9. Registra o resultado em `data/reports/AAAA-MM-DD-sync-notion.md` (arquivo novo, sem sobrescrever), separando operações factuais, estratégicas aprovadas, estratégicas recusadas ou pendentes, e bloqueadas.

### Fluxo de confirmação para mudança estratégica

1. **Detecção.** O `dhara-fit-scorer` ou um gatilho da rodada indica mudança de Decisão ou Status do funil que se enquadra como estratégica.
2. **Montagem.** O `edital-reporter` inclui a operação no payload com `tipo_alteracao: "estrategica"`. A sessão principal consulta a página atual no Notion para obter os valores vigentes.
3. **Prévia.** A sessão principal apresenta, para cada oportunidade:
   1. nome e link da oportunidade no Notion;
   2. valor atual e valor proposto de cada campo;
   3. motivo, evidência, data/hora e URL que justificam a alteração;
   4. impacto operacional (por exemplo, "passa a exigir preparação de documentos" ou "sai da fila de candidaturas");
   5. trecho exato que será acrescentado ao Histórico de alterações;
   6. payload exato do Notion que será enviado.
4. **Aprovação.** A pessoa usuária responde por oportunidade: aprovar, recusar ou adiar. Silêncio ou resposta ambígua conta como não aprovado. Uma aprovação vale somente para aquela prévia; se o conteúdo mudar, nova prévia.
5. **Gravação.** Somente o payload aprovado é enviado, com `update_properties` e, na mesma sequência, `insert_content` no fim da página com a entrada de histórico.
6. **Conferência.** Leitura de volta e registro no log de sincronização, com a aprovação e sua data/hora.
7. **Recusa ou adiamento.** Nada é gravado no Notion. A proposta fica registrada no log e volta em "Decisões humanas necessárias" na próxima rodada, se ainda fizer sentido.

## Modo agendado

Vale quando a rodada é executada por uma rotina agendada (execução autônoma na nuvem, sem pessoa usuária presente para confirmar). Execuções interativas continuam com a política de confirmação por escrita descrita em "Confirmação antes de gravar" e em "Fluxo de confirmação para mudança estratégica".

### Condições para gravar

A rotina agendada só grava no Notion quando, cumulativamente:

- `config/notion.yaml` tiver `modo_agendado.habilitado: true`;
- valerem as pré-condições de "Política de escrita" para o ambiente-alvo (sincronização habilitada, IDs resolvidos e `schema_verificado: true`);
- o schema lido na rodada com `notion-fetch` coincidir com este documento.

Com `modo_agendado.habilitado: false`, a rotina executa a rodada até o relatório local e não grava no Notion.

Se o schema lido divergir do documentado, a rodada **não grava nada no Notion** — nenhuma operação factual, nenhuma proposta e nenhuma página de relatório — e registra a falha conforme "Falhas de acesso".

### Modo sombra

Enquanto `config/notion.yaml` tiver `modo_agendado.alvo: teste`, a rotina grava **somente nas databases [TESTE]** (seção `teste` de `config/notion.yaml`), inclusive consultas de deduplicação e a página de relatório. A gravação em produção exige `alvo: producao`, definido por pessoa humana.

### Operações factuais

São gravadas sem confirmação. Nesta modalidade não se aplicam a apresentação em lote nem a confirmação na permissão da ferramenta descritas em "Níveis de atualização" e "Confirmação antes de gravar". Continuam valendo os gatilhos objetivos e os bloqueios do Status do funil, os campos fixos após a criação e a regra de somente acréscimo em Evidências e Histórico de alterações.

### Operações estratégicas

Não alteram Decisão nem Status do funil. Em vez disso, a sessão principal:

1. preenche "Decisão proposta" com o valor proposto (Aplicar, Avaliar com parceria, Monitorar ou Descartar);
2. preenche "Proposta estratégica" com valor atual, valor proposto, motivo, evidência, URL e data/hora;
3. marca "Revisão humana necessária";
4. acrescenta a proposta ao Histórico de alterações.

A regra de "Prazo vencido em candidatura em preparação" segue igual nos campos factuais, que são atualizados de imediato; a proposta estratégica correspondente vai para essas duas propriedades.

Enquanto a usuária não alterar Decisão, a proposta permanece. Se uma rodada posterior chegar a uma proposta diferente, atualiza as duas propriedades e registra a mudança no Histórico de alterações.

### Aprovação no Notion

A aprovação humana acontece no próprio Notion, quando a usuária altera Decisão. Na rodada seguinte, se Decisão estiver diferente do valor atual registrado em "Proposta estratégica", a sessão principal:

- respeita o valor definido pela usuária, seja ou não o valor proposto, e não o reverte nem o repropõe;
- limpa "Decisão proposta" e "Proposta estratégica" da proposta atendida;
- registra no Histórico de alterações o valor definido pela usuária e a limpeza da proposta, com data/hora.

**Recusa.** Se a usuária apagar "Decisão proposta", isso conta como recusa. A rodada seguinte limpa "Proposta estratégica", registra a recusa no Histórico de alterações e não repropõe o mesmo valor, salvo evidência nova, que deve ser citada na nova proposta.

**Alinhamento do Status do funil.** Quando a usuária alterar Decisão, a rodada seguinte alinha o Status do funil ao valor definido por ela — Aplicar → `APLICAR`, Avaliar com parceria → `AVALIAR_COM_PARCERIA`, Monitorar → `MONITORAR`, Descartar → `DESCARTADO` — e registra a mudança no Histórico de alterações. O alinhamento não é feito se o funil estiver em `EM_PREPARACAO`, `PRONTO_PARA_INSCRICAO`, `INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO` ou `NAO_APROVADO`.

### Criação

- Decisão `MONITORAR`: criação no nível factual, como nas execuções interativas.
- Decisão `APLICAR` ou `AVALIAR_COM_PARCERIA`: cria a página com Status do funil "Aguardando revisão humana", **Decisão vazia**, "Decisão proposta" e "Proposta estratégica" preenchidas (valor atual: vazio, página nova) e "Revisão humana necessária" marcada.
- Decisão `DESCARTAR`: não se cria.

### Exclusivamente humano

Inalterado. A rotina agendada nunca grava os itens de "Campos exclusivamente humanos".

### Limites por rodada

No máximo 10 criações e 20 atualizações de páginas na database de pipeline por rodada (`modo_agendado.limite_criacoes_por_rodada` e `modo_agendado.limite_atualizacoes_por_rodada`). O excedente não é gravado: vai para o relatório local, na seção "Sincronização com o Notion", como operações pendentes, e é reconsiderado na rodada seguinte. A página da database de Relatórios não entra nesses limites.

Quando houver mais operações que o limite, a ordem de gravação é esta, e o que não couber forma o excedente:

- **Criações:** por Prazo final crescente; em empate, por Score decrescente; oportunidades sem prazo por último.
- **Atualizações:** as que mudam Status validado, Status operacional, Status do funil ou prazo antes das demais.

### Deduplicação

Antes de gravar, a sessão principal consulta a database de pipeline do Notion do ambiente-alvo pela Chave de deduplicação, pelo Link oficial e pelo par Instituição + Identificador externo, conforme "Chave de deduplicação". Se houver mais de uma página, aquela oportunidade não é gravada e fica em `REVISAO` no relatório.

### Registro

O log `data/reports/AAAA-MM-DD-sync-notion.md` identifica a execução como agendada e registra o alvo (teste ou produção), as operações factuais gravadas, as propostas estratégicas preenchidas, as propostas atendidas e limpas, o excedente não gravado e as falhas.

### Persistência dos arquivos

Ao final de cada rodada agendada, a sessão principal faz commit e push dos arquivos novos de `data/reports/` na branch `claude/radar-rodadas`, criando-a se não existir, a partir da `main`. Nunca na `main` e nunca alterando arquivos fora de `data/reports/`. A página de relatório no Notion é o registro principal da rodada.

## Payloads preparados pelo `edital-reporter`

O `edital-reporter` pode preparar payloads, mas não grava no Notion:

- Arquivo: `data/reports/AAAA-MM-DD-notion-payload.json` (novo, com sufixo `-r2`, `-r3` se já existir).
- Conteúdo: uma lista de operações propostas, cada uma com `database` (`pipeline` ou `relatorios`), `operacao_proposta` (`criar_ou_atualizar`), `tipo_alteracao` (`factual` ou `estrategica`), `chave_deduplicacao`, `propriedades` (nomes das propriedades do Notion e valores já convertidos para rótulos), `historico` (entradas a acrescentar) e, para operações estratégicas, `motivo`, `evidencia`, `url_evidencia`, `data_hora_evidencia` e `impacto_operacional`.
- A decisão entre criar e atualizar, e a confirmação do nível de cada operação, são da sessão principal, depois da consulta ao Notion.
- A sessão principal valida o payload contra o schema e contra `config/notion.yaml` antes de apresentá-lo.

## Falhas de acesso

Se o Notion estiver inacessível, com erro de autenticação, IDs não resolvidos ou schema divergente:

- a rodada continua normalmente até o relatório local;
- nenhuma escrita parcial é tentada fora da aprovação;
- o relatório local registra a falha em "Limitações da rodada" e em "Sincronização com o Notion";
- o arquivo `data/reports/AAAA-MM-DD-sync-notion.md` registra a falha e as operações pendentes;
- a próxima rodada informa as pendências de sincronização anteriores.

## Primeira conexão operacional

Executar uma única vez, em uma branch de teste, antes da primeira sincronização real.

1. **Pré-requisito.** Patch principal aplicado e uma rodada piloto concluída sem Notion.
2. **Conectar.** No Claude Code, adicionar o servidor MCP e autenticar com a conta que tem acesso de edição às databases. Rodar `notion-get-tool-access` e registrar restrições.
3. **Localizar as databases.** Buscar "Pipeline de Editais — IFA Records" e "Relatórios do Radar — IFA Records".
   - Exatamente uma de cada: seguir.
   - Nenhuma: apresentar o DDL da seção "DDL de referência" e pedir aprovação explícita para criar.
   - Mais de uma: parar e pedir à pessoa usuária que indique a correta.
4. **Resolver os IDs.** Com `notion-fetch`, obter o ID da database e o `data_source_id` (`collection://...`) de cada uma. Propor o preenchimento de `config/notion.yaml`; a gravação do arquivo é feita por pessoa humana ou com aprovação.
5. **Verificar o schema.** Comparar propriedades, tipos e opções com este documento. Apresentar uma tabela de divergências. Divergências são corrigidas pela pessoa usuária ou em sessão de configuração aprovada; o radar não altera schema na operação. Ao final, marcar `schema_verificado: true` em `config/notion.yaml` (com aprovação).
6. **Criar o ambiente de teste.** Criar, com aprovação, duas databases de teste com o mesmo DDL, prefixadas com "[TESTE]", dentro de uma página de teste. Registrar seus IDs na seção `teste` de `config/notion.yaml`.
7. **Testar criação.** Preparar uma oportunidade fictícia claramente marcada ("[TESTE] Oportunidade fictícia — não é edital real", chave `teste:radar:0001`). Apresentar o payload, obter aprovação, criar na database de teste e conferir com `notion-fetch` cada propriedade e o corpo.
8. **Testar deduplicação.**
   - Repetir o mesmo payload: a consulta deve encontrar uma página e propor atualização, não criação.
   - Repetir com a URL alterada por `utm_source`, barra final e `www.`: a chave normalizada deve ser a mesma.
   - Conferir com `notion-query-data-sources` que existe só uma página com a chave `teste:radar:0001`.
9. **Testar histórico.** Atualizar o prazo com uma evidência fictícia nova. Conferir que a propriedade mudou e que o Histórico de alterações recebeu uma entrada nova, preservando as anteriores.
10. **Testar campos protegidos e níveis de atualização.**
    - Montar, sem gravar, um payload que tente definir Responsável ou Status do funil "Inscrito": a sessão principal deve recusar e retirar esses campos.
    - Simular uma mudança de Decisão de "Monitorar" para "Aplicar": deve gerar a prévia estratégica com os seis itens e só gravar após aprovação.
    - Simular a mesma mudança e responder "adiar": nada deve ser gravado e a proposta deve aparecer no log.
    - Simular `status_operacional` = `ENCERRADA` com fonte oficial: o funil deve ir para "Encerrado" pelo nível factual.
    - Colocar a página de teste em "Em preparação" manualmente e repetir a simulação anterior: os campos factuais (status validado e operacional, prioridade, revisão, última validação e histórico) devem ser atualizados, o funil e a Decisão devem permanecer, e deve sair um alerta crítico com proposta estratégica.
11. **Testar relatório.** Criar uma página na database de relatórios de teste, com relação para a oportunidade de teste. Tentar criar outra com a mesma chave: deve ser proposta com sufixo `-r2`, sem alterar a primeira.
12. **Testar falha.** Rodar uma sincronização em modo simulado com um `data_source_id` inválido: a rodada deve terminar, o relatório local deve registrar a falha e nada deve ser gravado.
13. **Encerrar os testes.** O radar não apaga páginas. Arquivar ou apagar as databases de teste é uma ação manual da pessoa usuária.
14. **Primeira sincronização real.** Lote pequeno (até cinco oportunidades), com revisão item a item.

## DDL de referência

Para uso somente na configuração inicial, com aprovação explícita, via `notion-create-database`. Criar primeiro a database de relatórios e usar o seu `data_source_id` na relação da database de pipeline.

```sql
CREATE TABLE (
  "Relatório" TITLE,
  "Chave do relatório" RICH_TEXT,
  "Tipo" SELECT('Diário':blue, 'Semanal':purple),
  "Data/hora da rodada" DATE,
  "Cobertura" SELECT('Brasil':green, 'Internacional':blue, 'Brasil e internacional':purple),
  "Modo de execução" SELECT('Subagentes formais':green, 'Modo agente único':orange),
  "Fontes consultadas" NUMBER,
  "Candidatas" NUMBER,
  "Validadas" NUMBER,
  "Descartadas" NUMBER,
  "Urgentes" NUMBER,
  "Em revisão" NUMBER,
  "Alta prioridade" NUMBER,
  "Propostas de URL" NUMBER,
  "Sincronização do pipeline" SELECT('Concluída':green, 'Parcial':yellow, 'Falhou':red, 'Não realizada':gray),
  "Arquivo local" RICH_TEXT,
  "Decisões humanas pendentes" CHECKBOX
)
```

```sql
CREATE TABLE (
  "Oportunidade" TITLE,
  "Chave de deduplicação" RICH_TEXT,
  "Identificador externo" RICH_TEXT,
  "Instituição" RICH_TEXT,
  "Tipo" SELECT('Edital':blue, 'Prêmio':yellow, 'Residência':purple, 'Festival':pink, 'Showcase':orange, 'Contratação':green, 'Intercâmbio':brown, 'Outro':gray),
  "Linguagem" MULTI_SELECT('Música':blue, 'Produção fonográfica':purple, 'Audiovisual musical':pink, 'Artes integradas':orange, 'Cultura digital':green, 'Formação de público':yellow, 'Outro':gray),
  "Modalidade" RICH_TEXT,
  "País" RICH_TEXT,
  "Estado/região" RICH_TEXT,
  "Cidade" RICH_TEXT,
  "Abrangência" SELECT('Municipal':gray, 'Estadual':brown, 'Nacional':green, 'Internacional':blue),
  "Cobertura" SELECT('Brasil':green, 'Internacional':blue),
  "Status do funil" SELECT('Descoberto':gray, 'Em validação':gray, 'Aguardando revisão humana':orange, 'Descartado':red, 'Monitorar':yellow, 'Avaliar com parceria':purple, 'Aplicar':green, 'Em preparação':blue, 'Pronto para inscrição':blue, 'Inscrito':green, 'Resultado aguardado':yellow, 'Aprovado':green, 'Não aprovado':red, 'Encerrado':gray),
  "Status validado" SELECT('Anunciada':gray, 'Aberta':green, 'Encerrada':red, 'Suspensa':orange, 'Prorrogada':yellow, 'Desconhecida':gray),
  "Status operacional" SELECT('Anunciada':gray, 'Aberta':green, 'Encerrada':red, 'Suspensa':orange, 'Prorrogada':yellow, 'Desconhecida':gray),
  "Decisão" SELECT('Aplicar':green, 'Avaliar com parceria':purple, 'Monitorar':yellow, 'Descartar':red),
  "Decisão proposta" SELECT('Aplicar':green, 'Avaliar com parceria':purple, 'Monitorar':yellow, 'Descartar':red),
  "Proposta estratégica" RICH_TEXT,
  "Prioridade" MULTI_SELECT('Urgente':red, 'Alta prioridade':orange, 'Revisão':yellow),
  "Revisão humana necessária" CHECKBOX,
  "Prazo final" DATE,
  "Fuso do prazo" RICH_TEXT,
  "Prazo original (texto)" RICH_TEXT,
  "Data da prorrogação" DATE,
  "Abertura" DATE,
  "Valor máximo" NUMBER,
  "Moeda" SELECT('BRL':green, 'EUR':blue, 'USD':gray, 'GBP':purple, 'Outra':gray),
  "PJ aceita" SELECT('Sim':green, 'Não':red, 'Não localizado':gray),
  "Exige parceiro local" SELECT('Sim':orange, 'Não':green, 'Não localizado':gray),
  "Fonte oficial confirmada" CHECKBOX,
  "Score" NUMBER,
  "Confiança" NUMBER FORMAT 'percent',
  "Motivo principal" RICH_TEXT,
  "Maior risco" RICH_TEXT,
  "Pendências" RICH_TEXT,
  "Próxima ação" RICH_TEXT,
  "Link oficial" URL,
  "Link de inscrição" URL,
  "Regulamento" URL,
  "Link de descoberta" URL,
  "Fonte de descoberta" SELECT('Oficial':green, 'PROSAS':blue, 'Parceiro':purple, 'Mídia':gray, 'Newsletter':gray, 'Rede social':gray),
  "Última validação" DATE,
  "Relatórios" RELATION('{{data_source_id_relatorios}}', DUAL 'Oportunidades'),
  "Responsável" PEOPLE,
  "Notas humanas" RICH_TEXT
)
```
