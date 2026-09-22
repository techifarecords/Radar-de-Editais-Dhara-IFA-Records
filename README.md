# Radar de Editais — Dhara / IFA Records

Sistema orientado por agentes Claude para descobrir, validar, priorizar e acompanhar editais, chamadas públicas, festivais, residências e oportunidades culturais para Dhara Guimarães, artista do casting da IFA Sounds LTDA, marca IFA Records.

O repositório é a fonte de verdade das regras do radar: perfil artístico, critérios de elegibilidade, fontes monitoradas, pipeline operacional, instruções dos subagentes e decisões técnicas. A sessão principal do Claude Code lê essas instruções, orquestra a rodada e delega as etapas a quatro subagentes especializados. O Notion é a camada operacional de registro: pipeline de oportunidades, relatórios e histórico, sincronizados somente pela sessão principal e com aprovação humana.

Este projeto monitora e organiza oportunidades. Ele não realiza automaticamente inscrições, assinaturas, pagamentos, envios de documentos, contratações ou outras ações irreversíveis.

## Objetivo

Encontrar oportunidades de financiamento, circulação e desenvolvimento artístico que tenham aderência à carreira de Dhara e aos projetos operados pela IFA Records, com cobertura de todo o Brasil e do exterior.

O sistema deve transformar informação dispersa em uma fila de decisões acionáveis:

```text
Fontes oficiais e setoriais
        ↓
Descoberta de candidatas
        ↓
Validação de fonte, status, prazo e regulamento
        ↓
Análise de elegibilidade para Dhara / IFA
        ↓
Score de aderência e recomendação
        ↓
Relatório, alertas e pipeline de inscrição
```

## Contexto de negócio

### Artista

Dhara Guimarães é cantora e compositora independente brasileira. O projeto prioritário é o álbum autoral “Nada disso é só meu”, que articula uma face acústica e intimista com uma face orientada por beats. A obra aborda relações, memória, cidade, intimidade, vivências individuais transformadas em narrativa coletiva e cultura brasileira contemporânea.

Possíveis entregas financiáveis ou programáveis incluem:

- Composição, pré-produção, gravação, mixagem e masterização de álbum, EP ou singles.
- Distribuição, lançamento, comunicação e estratégia de público.
- Videoclipe, live session, conteúdo audiovisual, fotografia e registro documental.
- Shows, circulação nacional, turnês, festivais, showcases e programações culturais.
- Residência artística, intercâmbio, mobilidade e apresentações internacionais.
- Artes integradas, multilinguagens, ações urbanas, comunicação visual, QR codes e formação de público.
- Acessibilidade cultural, contrapartidas educativas e ações de impacto cultural.

### Produtora e proponente

- Razão/identificação operacional: IFA Sounds LTDA.
- Nome comercial: IFA Records.
- Natureza conhecida: pessoa jurídica brasileira com CNPJ, enquadrada no Simples Nacional.
- Relação com a artista: Dhara possui contrato de agenciamento 360 com a IFA Sounds LTDA.

Regras fundamentais:

- Nunca tratar a IFA Sounds como MEI.
- Nunca inferir limites, tetos ou impedimentos próprios de MEI.
- Quando uma chamada aceitar ou exigir pessoa jurídica, empresa ou produtora cultural, avaliar a IFA Sounds como potencial proponente.
- Não inferir CNAE, data de abertura, endereço, inscrições municipais/estaduais, certidões, faturamento, dados bancários ou registros da empresa. Quando exigidos, registrar como pendência de validação humana.

### Cobertura territorial

A Dhara pode desenvolver, apresentar e circular projetos no Brasil inteiro e internacionalmente.

- Não limitar buscas a São Paulo.
- Pesquisar chamadas municipais, estaduais, nacionais e internacionais.
- Não descartar automaticamente oportunidades que exijam residência, sede, CNPJ local, instituição anfitriã ou parceiro territorial.
- Quando houver rota plausível — coprodução, parceria local, contratação artística, convite, entidade anfitriã ou projeto de circulação — classificar como AVALIAR_COM_PARCERIA e registrar os requisitos.

## Decisões do radar

Todos os valores internos (decisões, prioridades e status do funil) são escritos sem espaço e sem acento, por exemplo `EM_VALIDACAO` e `NAO_APROVADO`. Os relatórios exibem rótulos legíveis, como "Em validação" e "Não aprovado". A tabela completa está em `docs/04_PIPELINE_E_STATUS.md`.

| Decisão | Quando usar |
|---|---|
| APLICAR | Edital aberto, alta aderência e elegibilidade confirmada ou altamente provável, com prazo operacional viável. |
| AVALIAR_COM_PARCERIA | Boa aderência, mas depende de proponente/parceiro local, anfitrião, coprodução, convite, cofinanciamento ou checagem jurídica/documental. |
| MONITORAR | Chamada futura, anunciada, parcialmente aderente ou com informação essencial ainda ausente. |
| DESCARTAR | Encerrada, incompatível de forma clara, inelegível sem rota realista ou sem aderência ao escopo artístico. |

## Estrutura do repositório

```text
radar-editais-dhara/
├── README.md
├── CLAUDE.md
├── docs/
│   ├── 01_CONTEXTO_DHARA_IFA.md
│   ├── 02_CRITERIOS_DE_ELEGIBILIDADE.md
│   ├── 03_FONTES_DE_MONITORAMENTO.md
│   ├── 04_PIPELINE_E_STATUS.md
│   ├── 05_KIT_DOCUMENTAL.md
│   ├── 06_ORQUESTRACAO_DA_RODADA.md
│   └── 07_NOTION_OPERACAO.md
├── .claude/
│   └── agents/
│       ├── opportunity-discovery.md
│       ├── edital-validator.md
│       ├── dhara-fit-scorer.md
│       └── edital-reporter.md
├── data/
│   ├── inbox/
│   ├── validated/
│   ├── reports/
│   └── archive/
├── config/
│   ├── sources.yaml
│   ├── scoring.yaml
│   └── notion.yaml
└── templates/
    ├── weekly-report.md
    └── opportunity-record.md
```

## Papéis dos arquivos

| Caminho | Finalidade |
|---|---|
| `CLAUDE.md` | Regras globais que o Claude deve seguir em todas as sessões no repositório; define a sessão principal como orquestradora. |
| `docs/` | Contexto de negócio e regras operacionais detalhadas. `docs/06_ORQUESTRACAO_DA_RODADA.md` descreve a rodada conduzida pela sessão principal; `docs/07_NOTION_OPERACAO.md` define o uso do Notion. |
| `.claude/agents/` | Definições dos quatro subagentes formais. Cada arquivo representa um agente especializado. |
| `config/sources.yaml` | Lista versionada de fontes, frequência, categoria e nível de autoridade. |
| `config/scoring.yaml` | Pesos e regras configuráveis do score de aderência. |
| `config/notion.yaml` | IDs das databases do Notion e chave que habilita a sincronização. Sem segredos. |
| `data/` | Dados de trabalho: `inbox/`, `validated/`, `reports/` e `archive/`. Evitar versionar informações confidenciais. |
| `templates/` | Modelos de saídas padronizadas. |

## Agentes

A sessão principal do Claude Code é a orquestradora. Ela não é um subagente: no Claude Code, subagentes não podem criar outros subagentes. As regras da orquestração estão em `CLAUDE.md` e `docs/06_ORQUESTRACAO_DA_RODADA.md`.

| Papel | Quem executa / arquivo | Responsabilidade |
|---|---|---|
| Orquestração | Sessão principal (`CLAUDE.md`, `docs/06_ORQUESTRACAO_DA_RODADA.md`, `docs/07_NOTION_OPERACAO.md`) | Confere pré-condições, delega aos subagentes na ordem correta, normaliza e deduplica registros, consolida a execução e é a única que sincroniza com o Notion. |
| Descoberta | `.claude/agents/opportunity-discovery.md` | Localiza editais e oportunidades candidatas no Brasil e exterior. |
| Validação | `.claude/agents/edital-validator.md` | Confere fonte oficial, regulamento, status, prazo, valor, exigências e evidências. |
| Elegibilidade e score | `.claude/agents/dhara-fit-scorer.md` | Avalia aderência à Dhara/IFA, riscos, pendências e recomendação. |
| Relatórios e alertas | `.claude/agents/edital-reporter.md` | Produz alertas e relatório semanal e prepara payloads do Notion; pode gravar somente em `data/reports/` e não acessa o Notion. |

### Ordem obrigatória de execução

```text
1. opportunity-discovery   (subagente)
2. edital-validator        (subagente)
3. normalização e deduplicação pela sessão principal
4. dhara-fit-scorer        (subagente)
5. edital-reporter         (subagente)
6. consolidação pela sessão principal
7. sincronização com o Notion pela sessão principal, com aprovação humana
```

A sessão principal não deve simular agentes ausentes. Antes de iniciar uma rodada, ela deve verificar se todos os arquivos necessários existem e se os quatro subagentes aparecem em `/agents`.

## Fluxo de uma rodada

1. A sessão principal lê `CLAUDE.md`, os documentos em `docs/`, `config/` e o último relatório em `data/reports/`.
2. O agente de descoberta pesquisa fontes permitidas e registra oportunidades candidatas com URLs e evidências iniciais.
3. O agente de validação localiza a fonte oficial e o regulamento, confirma ou invalida status/prazo e extrai regras estruturadas.
4. A sessão principal normaliza e deduplica os registros validados.
5. O agente de elegibilidade calcula score, registra riscos e decide entre aplicar, avaliar parceria, monitorar ou descartar.
6. O agente de relatório produz alertas e um relatório em português do Brasil, gravado em `data/reports/`.
7. A sessão principal consolida o resultado.
8. Se a sincronização estiver habilitada em `config/notion.yaml`, a sessão principal verifica o schema, deduplica, apresenta o conteúdo exato, grava no Notion somente o que for aprovado e cria a página do relatório. Se o Notion estiver inacessível, a falha é registrada e a rodada termina normalmente.

## Critérios de prioridade

O score de aderência varia de 0 a 100 e deve ser explicável. A configuração detalhada fica em `config/scoring.yaml`.

| Critério | Pontuação máxima |
|---|---:|
| Aderência artística e de linguagem | 25 |
| Aderência de formato e escopo financiável | 20 |
| Elegibilidade da artista e da IFA Sounds | 15 |
| Cobertura territorial, circulação e internacionalização | 15 |
| Viabilidade financeira | 10 |
| Viabilidade pelo prazo | 5 |
| Confiabilidade e completude da informação | 5 |
| Valor estratégico | 5 |
| **Total** | **100** |

Aplicar penalidades explícitas por status não confirmado, edital encerrado, impedimento inequívoco de elegibilidade, baixa qualidade da fonte, prazo incompatível, ausência de dados essenciais ou incompatibilidade clara de escopo.

## Regras de validação

### Hierarquia de fontes

1. Edital, regulamento, retificação ou anexo oficial mais recente.
2. Página oficial da instituição realizadora.
3. Plataforma oficial de inscrição.
4. Comunicação institucional verificável.
5. Agregadores, imprensa, newsletters e redes sociais: apenas descoberta ou contexto.

### Status aberto

Uma oportunidade só pode ser marcada como `ABERTA` se houver evidência atual de pelo menos um dos itens abaixo:

- Prazo futuro inequívoco em fonte oficial.
- Status explícito de inscrições abertas.
- Formulário/plataforma oficial de inscrição disponível.
- Comunicação institucional recente que confirme abertura ou prorrogação.

Uma chamada `PRORROGADA` mantém esse valor em `status_validado` (histórico) e passa a ter `status_operacional` = `ABERTA` quando houver fonte oficial, prazo futuro inequívoco e inscrição disponível ou confirmada. As decisões e alertas usam o `status_operacional`. Detalhes em `docs/04_PIPELINE_E_STATUS.md`.

Quando prazo, horário, fuso, elegibilidade, valor ou regulamento não forem encontrados, o agente deve declarar o campo como não localizado, reduzir a confiança e marcar revisão humana. Nunca preencher lacunas por suposição.

## Fontes e escopo

O radar deve procurar, validar e acompanhar oportunidades de:

- Órgãos públicos federais, estaduais e municipais de cultura no Brasil inteiro.
- Programas de fomento, prêmios, bolsas, chamamentos e mecanismos públicos culturais.
- Programas de música, audiovisual musical, cultura digital, artes integradas e economia criativa.
- Sesc, SESI, fundações, institutos, centros culturais, instituições e programas corporativos.
- Festivais, showcases, programações, residências e mercados de música.
- Programas de mobilidade, intercâmbio e circulação internacional.
- Chamadas que aceitem artistas brasileiros, pessoas jurídicas brasileiras, coproduções ou parceiros anfitriões.

A lista operacional de fontes é mantida em `config/sources.yaml`. URLs ainda não verificadas ficam como `null`; o radar pode sugerir URLs no relatório, mas não edita o arquivo automaticamente. Uma fonte agregadora pode disparar descoberta, mas não pode ser a única base para afirmar que uma oportunidade está aberta ou elegível.

## Notion como camada operacional

O repositório continua sendo a fonte de verdade das regras. O Notion é o sistema de registro operacional: pipeline de oportunidades, relatórios semanais e alertas e histórico de alterações. A especificação completa está em `docs/07_NOTION_OPERACAO.md`.

| Database | Conteúdo |
|---|---|
| `Pipeline de Editais — IFA Records` | Uma página por oportunidade com decisão `APLICAR`, `AVALIAR_COM_PARCERIA` ou `MONITORAR`. Propriedades guardam o valor atual; o corpo da página guarda evidências e histórico de alterações. |
| `Relatórios do Radar — IFA Records` | Uma página nova por relatório semanal ou alerta, relacionada às oportunidades da rodada. |

Regras principais:

- Somente a sessão principal lê e grava no Notion; os subagentes não têm acesso. O `edital-reporter` apenas prepara payloads.
- Toda escrita exige IDs resolvidos em `config/notion.yaml`, schema verificado, consulta de deduplicação, apresentação do conteúdo exato e aprovação humana.
- A chave de deduplicação é a URL canônica da página oficial ou o identificador externo da chamada. O radar nunca cria duplicatas e nunca apaga registros.
- Evidências históricas nunca são sobrescritas: cada mudança acrescenta uma entrada ao histórico da página.
- Atualizações factuais (prazos, status da chamada, valores, links, score, prioridade e movimentos objetivos do funil) são gravadas sem prévia estratégica. Mudanças estratégicas de Decisão ou Status do funil (Aplicar, Avaliar com parceria, Descartar, Em preparação, Pronto para inscrição) exigem prévia e aprovação explícita.
- O radar nunca define `INSCRITO`, `RESULTADO_AGUARDADO`, `APROVADO` ou `NAO_APROVADO`, nem altera Responsável, Notas humanas ou dados sensíveis.
- Se o Notion estiver inacessível, a rodada continua e a falha fica registrada no relatório.
- As permissões locais de `.claude/settings.json` não controlam o Notion.

Antes da primeira sincronização real, siga o procedimento "Primeira conexão operacional" de `docs/07_NOTION_OPERACAO.md`.

## Como operar no Claude

### Antes da primeira rodada

1. Confirme que `CLAUDE.md` está na raiz do repositório.
2. Confirme que os sete documentos em `docs/` existem e estão atualizados.
3. Confirme que os quatro subagentes existem em `.claude/agents/`, possuem frontmatter YAML válido e aparecem em `/agents`.
4. Configure ou revise `config/sources.yaml` e `config/scoring.yaml`, e confira os modelos em `templates/`.
5. Execute uma rodada piloto, sem alterações externas e sem Notion (`sincronizacao.habilitada: false` em `config/notion.yaml`).
6. Siga a "Primeira conexão operacional" de `docs/07_NOTION_OPERACAO.md` antes de habilitar a sincronização.

### Prompt de auditoria inicial

Use no Claude Code dentro do repositório:

```text
Leia o repositório inteiro, especialmente CLAUDE.md, docs/, config/ e .claude/agents/.

Não execute pesquisa nem altere arquivos.

Confirme:
1. Quais subagentes foram encontrados, com nome, caminho e finalidade.
2. Se cada arquivo possui frontmatter reconhecível pelo ambiente atual.
3. Se há arquivos, regras ou configurações ausentes.
4. A ordem de delegação da sessão principal, conforme docs/06_ORQUESTRACAO_DA_RODADA.md.
5. Quais dados ainda precisam ser fornecidos manualmente antes da primeira rodada real.

Se encontrar problemas, apresente apenas um plano de correção e patches sugeridos. Aguarde minha aprovação antes de editar qualquer arquivo.
```

### Prompt para rodada piloto

```text
Execute uma rodada piloto do Radar de Editais — Dhara / IFA Records, seguindo docs/06_ORQUESTRACAO_DA_RODADA.md e delegando aos quatro subagentes.

Escopo:
- Pesquisar fontes permitidas no Brasil e internacionalmente.
- Priorizar música autoral, produção fonográfica, circulação, shows, festivais, showcases, residências, intercâmbio, audiovisual musical, artes integradas e acessibilidade.
- Considerar IFA Sounds/IFA Records como PJ brasileira com CNPJ no Simples Nacional; nunca como MEI.
- Não limitar a pesquisa a São Paulo.
- Validar informações em fonte oficial e regulamento antes de recomendar uma oportunidade.

Restrições:
- Não criar, editar ou enviar nada no Notion.
- Não realizar inscrições, envios, contatos, uploads, pagamentos ou ações externas.
- Não inventar dados ausentes.

Entregue relatório semanal em português do Brasil, com oportunidades urgentes, prioritárias, pendências e recomendações de próxima ação. O edital-reporter pode gravá-lo em data/reports/.
```

## Relatórios e alertas

Valores internos de prioridade: `URGENTE`, `ALTA_PRIORIDADE`, `REVISAO`. Regras completas em `docs/04_PIPELINE_E_STATUS.md`.

### URGENTE

Gerar alerta `URGENTE` somente quando os três critérios forem verdadeiros:

- `status_operacional` igual a `ABERTA`, validado em fonte oficial (inclui chamada prorrogada com novo prazo e inscrição confirmados).
- Decisão `APLICAR` ou `AVALIAR_COM_PARCERIA`.
- Prazo final em até sete dias.

### ALTA_PRIORIDADE

Marcar `ALTA_PRIORIDADE` quando:

- O score for igual ou superior a 75.
- `status_operacional` for `ABERTA`.
- O nível de confiança for igual ou superior a 0,70.

### REVISAO

Marcar `REVISAO` quando houver dado crítico ausente, divergência de fonte, dúvida de elegibilidade, exigência de parceiro/anfitrião, visto, idioma ou cofinanciamento, ou prazo/fuso ambíguo.

### Relatório semanal

Modelo: `templates/weekly-report.md`. Deve incluir:

- Pipeline por status e decisão.
- Ranking das 10 oportunidades mais relevantes.
- Calendário de prazos dos próximos 30 dias.
- Checklist documental consolidado.
- Blocos separados para oportunidades nacionais e internacionais.
- Padrões identificados e melhorias sugeridas para o kit de inscrição.

## Segurança e governança

- Não enviar inscrições, e-mails, mensagens, documentos, declarações ou formulários sem autorização humana explícita.
- Não realizar pagamentos, compras, contratações, assinaturas ou compromissos em nome da IFA ou da Dhara.
- Não registrar tokens, senhas, certificados, documentos societários, dados bancários ou dados pessoais sensíveis em arquivos versionados.
- Usar variáveis de ambiente para credenciais, quando uma integração aprovada exigir isso.
- Respeitar termos de uso, robots.txt, limites de requisição, copyright e regras de acesso das fontes.
- Não tentar burlar CAPTCHA, autenticação, paywalls, anti-bot ou bloqueios técnicos.
- Tratar a saída do agente como recomendação assistida: a decisão final de aplicação é humana.

## Manutenção recomendada

| Frequência | Atividade |
|---|---|
| Diária, em dias úteis | Rodada de descoberta, validação, score e alertas. |
| Semanal | Revisão de pipeline, prazos, parcerias e decisões de candidatura. |
| Mensal | Atualização das fontes, pesos do score e kit documental. |
| A cada edital prioritário | Criar uma pasta/dossiê de candidatura, checklist e versão adaptada do projeto. |
| A cada alteração estrutural | Revisar `CLAUDE.md`, `docs/06_ORQUESTRACAO_DA_RODADA.md`, `docs/07_NOTION_OPERACAO.md`, subagentes e documentos de contexto. |
| A cada mudança no schema do Notion | Atualizar `docs/07_NOTION_OPERACAO.md` e repetir a verificação de schema antes da próxima sincronização. |

## Estado atual do projeto

O repositório começa como uma camada de instruções e operação assistida pelo Claude. Ele pode evoluir futuramente para integrar bases estruturadas, automações de coleta, banco de dados e APIs, desde que sejam preservadas estas regras:

- validação em fonte oficial;
- evidência auditável;
- revisão humana para decisões críticas;
- cobertura nacional e internacional;
- avaliação correta da IFA Sounds como PJ no Simples Nacional.
