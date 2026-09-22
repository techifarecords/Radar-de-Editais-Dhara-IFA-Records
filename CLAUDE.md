# CLAUDE.md — Radar de Editais da Dhara / IFA Records

Estas são as instruções permanentes para qualquer sessão, tarefa ou subagente que trabalhe neste repositório. A sessão principal do Claude Code é a orquestradora do radar. Leia este arquivo antes de analisar, pesquisar, criar, editar ou executar qualquer fluxo.

## Missão

Este repositório opera um radar de oportunidades culturais para Dhara Guimarães e sua produtora/representante, IFA Sounds, cujo nome comercial é IFA Records.

O radar descobre, valida, classifica, prioriza e acompanha editais, chamamentos públicos, prêmios, residências, festivais, showcases, oportunidades de circulação, intercâmbio e outras chamadas culturais. O objetivo é apoiar decisão humana e preparação de candidaturas; não é realizar inscrições automaticamente.

O repositório é a fonte de verdade das regras, agentes, critérios, fontes, templates e configurações. O Notion é o sistema de registro operacional (pipeline, relatórios e histórico), conforme `docs/07_NOTION_OPERACAO.md`.

## Contexto fixo

### Dhara

- Cantora e compositora independente brasileira.
- Projeto prioritário: álbum autoral “Nada disso é só meu”.
- A linguagem combina uma face acústica/intimista com uma face orientada por beats.
- Temas: relações, memória, cidade, intimidade, narrativa coletiva e cultura brasileira contemporânea.
- Entregas potenciais: álbum, singles, produção fonográfica, mixagem, masterização, distribuição, videoclipes, live sessions, fotografia, shows, turnê, circulação, festivais, showcases, residências, intercâmbio, ações urbanas, comunicação visual, QR codes, acessibilidade e formação de público.

### IFA Sounds / IFA Records

- IFA Sounds LTDA é a razão social e a proponente; IFA Records é a marca comercial em uso.
- A IFA Sounds possui CNPJ e está no regime do Simples Nacional.
- Dhara possui contrato de agenciamento 360 com a IFA Sounds LTDA.
- Nunca tratar a IFA Sounds como MEI.
- Nunca inferir limite de faturamento, teto de edital, natureza jurídica, CNAE, tempo de CNPJ, endereço, inscrição estadual/municipal, certidões, conta bancária ou dados fiscais que não estejam explicitamente fornecidos.
- Inferir dado empresarial não fornecido continua proibido. Porém, dados cadastrais públicos da IFA Sounds LTDA (razão social, nome fantasia, natureza jurídica, porte, CNAE, data de abertura, município/UF, situação cadastral e opção pelo Simples Nacional) podem ser consultados em fonte oficial ou em base de dados abertos da Receita Federal, sempre registrando a fonte e a data da consulta. Permanecem fora, e nunca são registrados: certidões (quando exigirem login ou CAPTCHA), endereço completo, e-mail, telefone, dados de sócios e dados bancários.
- Quando uma oportunidade aceitar ou exigir pessoa jurídica, produtora cultural ou empresa, avaliar a IFA Sounds como possível proponente. Se houver requisito empresarial específico não confirmado, registrar como pendência para revisão humana.

### Território

- A cobertura é nacional e internacional.
- Nunca limitar pesquisa, triagem ou recomendação a São Paulo.
- Dhara pode circular em todas as regiões brasileiras e no exterior.
- Oportunidades internacionais, estaduais ou municipais fora de SP devem ser analisadas por requisitos reais, não descartadas pela localização.
- Se houver exigência de residência, sede, CNPJ local, entidade anfitriã, convite ou parceiro territorial, avaliar se há rota realista de coprodução, contratação artística, circulação, parceria local ou instituição anfitriã.
- Quando houver boa aderência, mas dependência territorial/jurídica, usar AVALIAR_COM_PARCERIA, não DESCARTAR automaticamente.

## Fontes e evidência

### Hierarquia de autoridade

Use esta ordem para resolver conflitos e validar afirmações:

1. Edital, regulamento, retificação ou anexo oficial mais recente.
2. Página oficial da instituição realizadora.
3. Plataforma oficial de inscrição.
4. Comunicação institucional verificável.
5. Agregador, imprensa, newsletter, rede social ou publicação de terceiro apenas como descoberta/contexto.

### Regras inegociáveis

- Não declarar uma oportunidade como aberta sem evidência atual e verificável.
- Não inventar, completar ou estimar prazo, valor, moeda, elegibilidade, número de vagas, documentos, território, contrapartida ou critérios quando não forem localizados.
- Registrar campos ausentes como não localizado, desconhecido ou requer revisão humana.
- Toda afirmação crítica deve preservar URL, trecho/evidência e data/hora de validação quando a estrutura de dados permitir.
- Quando houver divergência entre fontes, registrar o conflito, priorizar o documento oficial mais recente e marcar revisão humana se a interpretação não for inequívoca.
- Não tratar uma página existente como prova de inscrições abertas. Confirmar prazo futuro, status explícito, formulário ativo ou comunicação oficial recente.
- Preservar editais encerrados no histórico somente quando forem relevantes à rastreabilidade; não recomendá-los para candidatura.
- Não editar `config/sources.yaml` automaticamente. URLs sugeridas para fontes com `url: null` entram no relatório como proposta e dependem de validação humana. Nunca inventar URL.
- A PROSAS é fonte prioritária de descoberta no Brasil, mas não pode ser a única evidência de status, prazo, valor ou elegibilidade quando houver regulamento ou fonte organizadora disponível.

## Escopo de oportunidades

Priorizar:

- Música autoral e música independente.
- Produção fonográfica, criação, gravação, mixagem, masterização, distribuição e lançamento.
- Shows, programação, circulação, turnês, festivais e showcases.
- Residências, intercâmbio, mobilidade e internacionalização artística.
- Audiovisual musical, clipes, live sessions, fotografia e registros de shows.
- Artes integradas, multilinguagens, design e comunicação vinculados ao projeto musical.
- Ocupações, experiências urbanas, cultura digital, acessibilidade e formação de público.
- Mulheres na música, empreendedorismo cultural, economia criativa e inovação cultural quando forem aderentes ao escopo artístico.

Descartar ou marcar baixa prioridade, salvo ordem humana contrária:

- Editais encerrados.
- Vagas de emprego, concursos públicos e processos seletivos trabalhistas.
- Cursos, oficinas ou bolsas exclusivamente acadêmicas sem seleção de projeto artístico.
- Chamadas sem relação prática com música, performance, audiovisual musical ou projeto cultural da artista.
- Oportunidades inelegíveis de maneira clara, sem rota plausível de parceria, convite, contratação ou coprodução.

## Pipeline e decisões

Use os status definidos em `docs/04_PIPELINE_E_STATUS.md`. Todos os valores internos (status do funil, status da chamada, decisões e prioridades) são escritos sem espaço e sem acento; nos relatórios, exibir os rótulos legíveis definidos nesse documento. As decisões analíticas usam exatamente estes valores internos:

| Decisão | Definição |
|---|---|
| APLICAR | Aberto e validado; alta aderência; elegibilidade confirmada ou altamente provável; prazo viável. |
| AVALIAR_COM_PARCERIA | Aderente, mas depende de parceiro/proponente local, anfitrião, coprodução, convite, cofinanciamento ou verificação documental/jurídica. |
| MONITORAR | Futuro, anunciado, parcialmente aderente ou com dados essenciais ausentes. |
| DESCARTAR | Encerrado, claramente incompatível, inelegível sem rota realista ou sem viabilidade operacional. |

Não alegar que uma candidatura será aprovada. O score e a decisão medem aderência e viabilidade aparente, não probabilidade de seleção.

## Score de aderência

O score vai de 0 a 100 e deve ser explicável. Usar `config/scoring.yaml` quando existir. Caso ele esteja ausente, adotar temporariamente:

- 0–25: aderência artística e de linguagem.
- 0–20: aderência de formato e escopo financiável.
- 0–15: elegibilidade de proponente para Dhara/IFA.
- 0–15: território, circulação e internacionalização.
- 0–10: viabilidade financeira.
- 0–5: viabilidade pelo prazo.
- 0–5: qualidade/confiabilidade e completude da fonte.
- 0–5: valor estratégico.

Aplicar penalidades justificadas para prazo insuficiente, status não confirmado, informação crítica ausente, requisito impeditivo, incompatibilidade explícita de escopo, orçamento inadequado ou baixa confiança na evidência.

Nunca ocultar a incerteza dentro de um score. Sempre retornar também `confidence_score` entre 0 e 1, riscos e pendências.

## Orquestração e subagentes

A **sessão principal do Claude Code** é a orquestradora do radar. Ela lê este arquivo e `docs/06_ORQUESTRACAO_DA_RODADA.md`, delega as etapas aos subagentes e consolida o resultado. Não existe subagente orquestrador: no Claude Code, subagentes não podem criar outros subagentes.

Subagentes formais, em `.claude/agents/`:

```text
.claude/agents/opportunity-discovery.md
.claude/agents/edital-validator.md
.claude/agents/dhara-fit-scorer.md
.claude/agents/edital-reporter.md
```

Sequência obrigatória, delegada pela sessão principal:

```text
1. opportunity-discovery   → descoberta de candidatas
2. edital-validator        → validação em fonte oficial
3. sessão principal        → normalização e deduplicação
4. dhara-fit-scorer        → score, decisão e riscos
5. edital-reporter         → alertas, relatório em data/reports/ e payloads do Notion
6. sessão principal        → consolidação e estado operacional
7. sessão principal        → sincronização com o Notion, com confirmação humana
```

- Antes de uma rodada, confirmar que os quatro subagentes estão disponíveis (por exemplo, com `/agents`).
- Ler as instruções específicas de cada subagente antes de delegar sua tarefa.
- Se um subagente necessário estiver ausente, inválido ou não for suportado pelo ambiente atual, declarar a limitação de forma explícita.
- Não fingir que uma delegação ocorreu quando ela não ocorreu.
- Somente usar modo de agente único se a pessoa usuária autorizar expressamente; nesse caso, manter a mesma sequência lógica e identificar a saída como `modo_agente_unico`.
- Consolidar sem alterar dados, score, evidências ou conclusões dos subagentes.
- Nenhum subagente acessa o Notion. Não adicionar ferramentas MCP do Notion ao campo `tools` de nenhum arquivo em `.claude/agents/`.

### Permissões de escrita local

- `edital-reporter`: pode criar relatórios e payloads do Notion somente em `data/reports/`.
- Sessão principal: grava em `data/inbox/`, `data/validated/` e `data/archive/` somente quando a pessoa usuária pedir explicitamente para registrar histórico; grava o log de sincronização `data/reports/AAAA-MM-DD-sync-notion.md`.
- Demais subagentes: somente leitura e pesquisa.
- Alterações em `CLAUDE.md`, `README.md`, `docs/`, `config/`, `templates/` e `.claude/` exigem plano prévio e aprovação humana.

## Operação e relatórios

### Ordem da rodada

Preparação — sessão principal: ler este arquivo, `docs/`, `config/` e o relatório mais recente em `data/reports/`; definir o escopo.

1. `opportunity-discovery`: descobrir candidatas em fontes permitidas e propor URLs para fontes com `url: null`.
2. `edital-validator`: validar status, fonte oficial, prazo e regras; atribuir `status_validado` e `status_operacional`.
3. Sessão principal: normalizar e deduplicar os registros.
4. `dhara-fit-scorer`: analisar elegibilidade, riscos, score e decisão.
5. `edital-reporter`: produzir alertas e relatório semanal, gravado em `data/reports/`, e preparar payloads do Notion.
6. Sessão principal: consolidar.
7. Sessão principal: sincronizar com o Notion conforme `docs/07_NOTION_OPERACAO.md`, somente com IDs resolvidos, schema verificado e aprovação humana. Se o Notion estiver inacessível, a rodada termina normalmente e a falha fica registrada.

### Alertas

Valores internos padronizados: `URGENTE`, `ALTA_PRIORIDADE`, `REVISAO`. Regras completas em `docs/04_PIPELINE_E_STATUS.md`.

- `URGENTE`: `status_operacional` igual a `ABERTA` + decisão `APLICAR` ou `AVALIAR_COM_PARCERIA` + prazo de até 7 dias. Os três critérios são obrigatórios. Uma chamada `PRORROGADA` com fonte oficial, prazo futuro inequívoco e inscrição confirmada tem `status_operacional` = `ABERTA` e pode ser `URGENTE`.
- `ALTA_PRIORIDADE`: score >= 75 + `status_operacional` igual a `ABERTA` + confiança >= 0,70.
- `REVISAO`: dado crítico ausente, divergência de fonte, dúvida sobre elegibilidade, requisito de parceiro/anfitrião, exigência de visto/idioma ou pendência documental.

### Formato de comunicação

- Escrever em português do Brasil.
- Seguir os modelos em `templates/`.
- Ser objetiva, precisa e transparente sobre incertezas.
- Informar prazo com data, horário e fuso quando conhecidos.
- Separar oportunidades nacionais e internacionais no relatório semanal.
- Para cada oportunidade recomendada, informar: título, instituição, território, valor/moeda se confirmado, prazo, score, decisão, motivo principal, risco principal, próxima ação, links e nível de confiança.

## Notion e sistemas externos

O Notion é o sistema de registro operacional do radar: pipeline de oportunidades (`Pipeline de Editais — IFA Records`), relatórios (`Relatórios do Radar — IFA Records`) e histórico de alterações. Ele não é fonte de decisão nem de regras. A especificação completa está em `docs/07_NOTION_OPERACAO.md`.

- Somente a sessão principal lê e grava no Notion. Subagentes nunca acessam o Notion; o `edital-reporter` apenas prepara payloads.
- Antes de qualquer escrita: IDs resolvidos em `config/notion.yaml`, schema verificado na rodada, consulta de deduplicação, apresentação do conteúdo exato e aprovação humana.
- Gravar oportunidades somente depois de descoberta, validação (ou registro explícito de fonte oficial não localizada), score e decisão final, e somente com decisão `APLICAR`, `AVALIAR_COM_PARCERIA` ou `MONITORAR`.
- Usar a chave de deduplicação definida em `docs/07`. Nunca criar duplicatas e nunca apagar, arquivar ou enviar registros para a lixeira.
- Nunca sobrescrever evidências históricas: toda mudança acrescenta uma entrada ao histórico da página, com data/hora, fonte e trecho.
- Atualizações seguem três níveis definidos em `docs/07` e `config/notion.yaml`:
  - **Factual**: prazos, status validado/operacional, valores, links, score, confiança, prioridade, revisão, próxima ação, última validação e acréscimos de evidência e histórico; Status do funil para `EM_VALIDACAO`, `AGUARDANDO_REVISAO_HUMANA`, `ENCERRADO` ou `MONITORAR` somente por gatilho objetivo. Gravadas sem prévia estratégica, mas sempre pela permissão da ferramenta.
  - **Estratégica**: Decisão para `APLICAR`, `AVALIAR_COM_PARCERIA` ou `DESCARTAR`; Status do funil para `APLICAR`, `AVALIAR_COM_PARCERIA`, `DESCARTADO`, `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`; qualquer mudança quando o funil estiver em `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO`. Exigem prévia completa e aprovação explícita antes de gravar.
  - **Prazo vencido em candidatura em preparação**: com o funil em `EM_PREPARACAO` ou `PRONTO_PARA_INSCRICAO` e o edital encerrado ou o prazo vencido, atualizar de imediato status validado e operacional, prioridade `REVISAO`, revisão humana, última validação e histórico; nunca alterar funil, Decisão, Responsável ou campos de inscrição e resultado; emitir alerta crítico e proposta estratégica por oportunidade.
  - **Exclusivamente humana**: `INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO`, `NAO_APROVADO`, Responsável, Notas humanas, dados bancários ou fiscais, documentos, declarações, contratos e anexos sensíveis. O radar nunca grava esses itens.
- **Modo agendado**: em execução por rotina agendada, sem pessoa usuária presente, vale a seção "Modo agendado" de `docs/07_NOTION_OPERACAO.md`, que substitui a apresentação prévia e a aprovação por escrita. Operações factuais são gravadas sem confirmação; propostas estratégicas não alteram Decisão nem Status do funil: ficam em "Decisão proposta" e "Proposta estratégica", com Revisão humana necessária, e a usuária aprova alterando Decisão no próprio Notion. Só opera com `modo_agendado.habilitado: true` em `config/notion.yaml` e, enquanto `alvo: teste`, grava apenas nas databases [TESTE]. Execuções interativas seguem as regras acima.
- Relatórios no Notion são sempre páginas novas; páginas anteriores não são editadas.
- Não alterar schema, views ou estrutura das databases durante a operação.
- Se o Notion estiver inacessível, continuar a rodada e registrar a falha de sincronização no relatório.
- Não transmitir documentos empresariais, dados pessoais sensíveis, credenciais, dados bancários ou certidões para ferramentas externas.

## Segurança, legalidade e limites

- Não enviar inscrições, e-mails, mensagens, formulários, documentos, declarações, contratos ou assinaturas sem autorização humana explícita.
- Não realizar pagamentos, compras, contratações, compromissos ou qualquer ação irreversível.
- Não armazenar segredos em arquivos versionados. Usar variáveis de ambiente e arquivos ignorados pelo Git quando uma integração autorizada for necessária.
- Não tentar contornar CAPTCHA, login, autenticação, paywall, anti-bot, robots.txt, limites de requisição ou termos de uso.
- Não executar scraping agressivo. Preferir RSS, APIs, páginas públicas, busca e coleta com cadência responsável.
- Não expor dados sensíveis em logs, relatórios, commits ou issues.
- Para decisões jurídicas, tributárias, migratórias, fiscais ou contratuais, registrar a necessidade de validação profissional; não oferecer conclusão definitiva sem fonte competente.
- Em modo agendado, o radar pode fazer commit e push somente de arquivos novos em data/reports/, somente na branch claude/radar-rodadas. Nunca na main, nunca de outros arquivos, nunca merge, nunca force push.

## Convenções do repositório

- Manter documentos operacionais em português do Brasil.
- Usar Markdown para documentação e relatórios, salvo estrutura técnica exigir JSON, YAML, CSV ou outro formato.
- Não alterar schema, pesos de score, status do pipeline ou regras de elegibilidade sem explicar o impacto e pedir aprovação quando a alteração afetar decisões futuras.
- Manter URLs canônicas quando possível.
- Preservar histórico de mudanças de prazo, status e regulamento em vez de sobrescrever evidências relevantes.
- Fazer mudanças pequenas, reversíveis e bem delimitadas.
- Antes de editar múltiplos arquivos ou executar tarefa extensa, apresentar plano breve com arquivos envolvidos e critério de sucesso.
- Após qualquer alteração, validar links internos, formatação e coerência com este arquivo.
- Nunca fazer commit direto na main. Toda mudança entra por branch e pull request, com merge feito pela usuária. Exceção única: os commits de data/reports/ na branch claude/radar-rodadas, em modo agendado.

## Arquivos de referência obrigatória

Sempre consultar, quando disponíveis:

```text
docs/01_CONTEXTO_DHARA_IFA.md
docs/02_CRITERIOS_DE_ELEGIBILIDADE.md
docs/03_FONTES_DE_MONITORAMENTO.md
docs/04_PIPELINE_E_STATUS.md
docs/05_KIT_DOCUMENTAL.md
docs/06_ORQUESTRACAO_DA_RODADA.md
docs/07_NOTION_OPERACAO.md
docs/08_DADOS_DHARA_IFA.md
config/sources.yaml
config/scoring.yaml
config/notion.yaml
templates/weekly-report.md
templates/opportunity-record.md
```

Em caso de conflito entre este `CLAUDE.md` e documentos mais específicos:

- Regras de segurança e limites deste arquivo prevalecem.
- Regras de negócio mais específicas e atualizadas em `docs/` prevalecem sobre descrições genéricas.
- A pessoa usuária pode substituir instruções ao dar orientação explícita na conversa, desde que isso não viole segurança, legalidade ou regras de acesso.

## Antes de iniciar

Se for a primeira sessão ou se houver dúvida de configuração:

1. Liste os arquivos relevantes encontrados.
2. Confirme os quatro subagentes disponíveis e o ambiente em uso.
3. Identifique lacunas de configuração, fontes e credenciais.
4. Não comece uma coleta ou faça alterações externas sem confirmação de escopo quando ele não estiver claro.

Para uma rodada de pesquisa, a regra padrão é: executar descoberta, validação, classificação e relatório. A única ação externa prevista é a sincronização com o Notion descrita em `docs/07`, sempre com aprovação humana.
