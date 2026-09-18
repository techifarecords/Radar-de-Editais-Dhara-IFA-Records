Radar de Editais — Dhara / IFA Records
Sistema orientado por agentes Claude para descobrir, validar, priorizar e acompanhar editais, chamadas públicas, festivais, residências e oportunidades culturais para Dhara Guimarães, artista do casting da IFA Sounds, cujo nome comercial é IFA Records.

O repositório é a fonte de verdade das regras do radar: perfil artístico, critérios de elegibilidade, fontes monitoradas, pipeline operacional, instruções dos subagentes e decisões técnicas. O Claude Code lê essas instruções e coordena os agentes especializados; o Notion pode ser usado opcionalmente como painel de acompanhamento humano.

Este projeto monitora e organiza oportunidades. Ele não realiza automaticamente inscrições, assinaturas, pagamentos, envios de documentos, contratações ou outras ações irreversíveis.

Objetivo
Encontrar oportunidades de financiamento, circulação e desenvolvimento artístico que tenham aderência à carreira de Dhara e aos projetos operados pela IFA Records, com cobertura de todo o Brasil e do exterior.

O sistema deve transformar informação dispersa em uma fila de decisões acionáveis:

text
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
Contexto de negócio
Artista
Dhara Guimarães é cantora, compositora e produtora musical independente brasileira. O projeto prioritário é o álbum autoral “Nada disso é só meu”, que articula uma face acústica e intimista com uma face orientada por beats. A obra aborda relações, memória, cidade, intimidade, vivências individuais transformadas em narrativa coletiva e cultura brasileira contemporânea.

Possíveis entregas financiáveis ou programáveis incluem:

Composição, pré-produção, gravação, mixagem e masterização de álbum, EP ou singles.

Distribuição, lançamento, comunicação e estratégia de público.

Videoclipe, live session, conteúdo audiovisual, fotografia e registro documental.

Shows, circulação nacional, turnês, festivais, showcases e programações culturais.

Residência artística, intercâmbio, mobilidade e apresentações internacionais.

Artes integradas, multilinguagens, ações urbanas, comunicação visual, QR codes e formação de público.

Acessibilidade cultural, contrapartidas educativas e ações de impacto cultural.

Produtora e proponente
Razão/identificação operacional: IFA Sounds.

Nome comercial: IFA Records.

Natureza conhecida: pessoa jurídica brasileira com CNPJ, enquadrada no Simples Nacional.

Relação com a artista: Dhara possui contrato com a IFA Sounds.

Regras fundamentais:

Nunca tratar a IFA Sounds como MEI.

Nunca inferir limites, tetos ou impedimentos próprios de MEI.

Quando uma chamada aceitar ou exigir pessoa jurídica, empresa ou produtora cultural, avaliar a IFA Sounds como potencial proponente.

Não inferir CNAE, data de abertura, endereço, inscrições municipais/estaduais, certidões, faturamento, dados bancários ou registros da empresa. Quando exigidos, registrar como pendência de validação humana.

Cobertura territorial
A Dhara pode desenvolver, apresentar e circular projetos no Brasil inteiro e internacionalmente.

Não limitar buscas a São Paulo.

Pesquisar chamadas municipais, estaduais, nacionais e internacionais.

Não descartar automaticamente oportunidades que exijam residência, sede, CNPJ local, instituição anfitriã ou parceiro territorial.

Quando houver rota plausível — coprodução, parceria local, contratação artística, convite, entidade anfitriã ou projeto de circulação — classificar como AVALIAR_COM_PARCERIA e registrar os requisitos.

Decisões do radar
Decisão	Quando usar
APLICAR	Edital aberto, alta aderência e elegibilidade confirmada ou altamente provável, com prazo operacional viável.
AVALIAR_COM_PARCERIA	Boa aderência, mas depende de proponente/parceiro local, anfitrião, coprodução, convite, cofinanciamento ou checagem jurídica/documental.
MONITORAR	Chamada futura, anunciada, parcialmente aderente ou com informação essencial ainda ausente.
DESCARTAR	Encerrada, incompatível de forma clara, inelegível sem rota realista ou sem aderência ao escopo artístico.
Estrutura do repositório
text
radar-editais-dhara/
├── README.md
├── CLAUDE.md
├── docs/
│   ├── 01_CONTEXTO_DHARA_IFA.md
│   ├── 02_CRITERIOS_DE_ELEGIBILIDADE.md
│   ├── 03_FONTES_DE_MONITORAMENTO.md
│   ├── 04_PIPELINE_E_STATUS.md
│   └── 05_KIT_DOCUMENTAL.md
├── .claude/
│   └── agents/
│       ├── edital-orchestrator.md
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
│   └── scoring.yaml
└── templates/
    ├── daily-report.md
    ├── weekly-report.md
    └── opportunity-record.md
Papéis dos arquivos
Caminho	Finalidade
CLAUDE.md	Regras globais que o Claude deve seguir em todas as sessões no repositório.
docs/	Contexto de negócio e regras operacionais detalhadas.
.claude/agents/	Definições individuais dos subagentes. Cada arquivo representa um agente especializado.
config/sources.yaml	Lista versionada de fontes, frequência, categoria e nível de autoridade.
config/scoring.yaml	Pesos e regras configuráveis do score de aderência.
data/	Dados de trabalho, relatórios e histórico. Evitar versionar informações confidenciais.
templates/	Modelos de saídas padronizadas.
Agentes
O sistema é organizado em agentes especializados, coordenados pelo orquestrador.

Agente	Arquivo	Responsabilidade
Orquestrador	.claude/agents/edital-orchestrator.md	Confere pré-condições, chama os demais agentes na ordem correta e consolida a execução.
Descoberta	.claude/agents/opportunity-discovery.md	Localiza editais e oportunidades candidatas no Brasil e exterior.
Validação	.claude/agents/edital-validator.md	Confere fonte oficial, regulamento, status, prazo, valor, exigências e evidências.
Elegibilidade e score	.claude/agents/dhara-fit-scorer.md	Avalia aderência à Dhara/IFA, riscos, pendências e recomendação.
Relatórios e alertas	.claude/agents/edital-reporter.md	Produz alertas, relatório diário e revisão semanal.
Ordem obrigatória de execução
text
1. opportunity-discovery
2. edital-validator
3. dhara-fit-scorer
4. edital-reporter
5. edital-orchestrator consolida o resultado
O orquestrador não deve simular agentes ausentes. Antes de iniciar uma rodada, ele deve verificar se todos os arquivos necessários existem e se o frontmatter de cada subagente é reconhecido pelo ambiente Claude em uso.

Fluxo de uma rodada
O orquestrador lê CLAUDE.md, os documentos em docs/, a configuração de fontes e o último relatório disponível.

O agente de descoberta pesquisa fontes permitidas e registra oportunidades candidatas com URLs e evidências iniciais.

O agente de validação localiza a fonte oficial e o regulamento, confirma ou invalida status/prazo e extrai regras estruturadas.

O agente de elegibilidade calcula score, registra riscos e decide entre aplicar, avaliar parceria, monitorar ou descartar.

O agente de relatório produz alertas e um relatório em português do Brasil.

Se o Notion estiver conectado e autorizado, apenas os itens aprovados para acompanhamento podem ser registrados no pipeline, sem qualquer submissão automática.

Critérios de prioridade
O score de aderência varia de 0 a 100 e deve ser explicável. A configuração detalhada deve ficar em config/scoring.yaml.

Critério	Pontuação máxima
Aderência artística e de linguagem	25
Aderência de formato e escopo financiável	20
Elegibilidade da artista e da IFA Sounds	15
Cobertura territorial, circulação e internacionalização	15
Viabilidade financeira	10
Viabilidade pelo prazo	5
Confiabilidade e completude da informação	5
Valor estratégico	5
Total	100
Aplicar penalidades explícitas por status não confirmado, edital encerrado, impedimento inequívoco de elegibilidade, baixa qualidade da fonte, prazo incompatível, ausência de dados essenciais ou incompatibilidade clara de escopo.

Regras de validação
Hierarquia de fontes
Edital, regulamento, retificação ou anexo oficial mais recente.

Página oficial da instituição realizadora.

Plataforma oficial de inscrição.

Comunicação institucional verificável.

Agregadores, imprensa, newsletters e redes sociais: apenas descoberta ou contexto.

Status aberto
Uma oportunidade só pode ser marcada como ABERTA se houver evidência atual de pelo menos um dos itens abaixo:

Prazo futuro inequívoco em fonte oficial.

Status explícito de inscrições abertas.

Formulário/plataforma oficial de inscrição disponível.

Comunicação institucional recente que confirme abertura ou prorrogação.

Quando prazo, horário, fuso, elegibilidade, valor ou regulamento não forem encontrados, o agente deve declarar o campo como não localizado, reduzir a confiança e marcar revisão humana. Nunca preencher lacunas por suposição.

Fontes e escopo
O radar deve procurar, validar e acompanhar oportunidades de:

Órgãos públicos federais, estaduais e municipais de cultura no Brasil inteiro.

Programas de fomento, prêmios, bolsas, chamamentos e mecanismos públicos culturais.

Programas de música, audiovisual musical, cultura digital, artes integradas e economia criativa.

Sesc, SESI, fundações, institutos, centros culturais, instituições e programas corporativos.

Festivais, showcases, programações, residências e mercados de música.

Programas de mobilidade, intercâmbio e circulação internacional.

Chamadas que aceitem artistas brasileiros, pessoas jurídicas brasileiras, coproduções ou parceiros anfitriões.

A lista operacional de fontes deve ser mantida em config/sources.yaml. Uma fonte agregadora pode disparar descoberta, mas não pode ser a única base para afirmar que uma oportunidade está aberta ou elegível.

Notion opcional
O Notion é uma camada de acompanhamento, não o motor de decisão. Use-o para registrar itens que passaram pela análise e exigem ação humana.

Banco sugerido
Nome: Pipeline de Editais — IFA Records

Propriedades recomendadas:

Edital / oportunidade

Status

Decisão

Score

Urgência

Instituição

País

Estado/região

Modalidade

Prazo

Moeda

Valor máximo

PJ aceita?

Exige parceiro local?

Fonte oficial confirmada?

Confiança

Link oficial

Regulamento

Próxima ação

Responsável

Revisão humana necessária?

Última validação

Observações e evidências

Antes de permitir criação ou atualização no Notion, estabeleça explicitamente quais campos o Claude pode editar. Não autorize o Claude a mudar INSCRITO, APROVADO, NÃO_APROVADO ou dados sensíveis sem uma decisão humana explícita.

Como operar no Claude
Antes da primeira rodada
Confirme que CLAUDE.md está na raiz do repositório.

Confirme que os cinco documentos em docs/ existem e estão atualizados.

Confirme que cada agente existe em .claude/agents/ e possui frontmatter YAML válido.

Configure ou revise config/sources.yaml e config/scoring.yaml.

Execute uma rodada piloto, sem alterações externas e sem Notion.

Prompt de auditoria inicial
Use no Claude Code dentro do repositório:

text
Leia o repositório inteiro, especialmente CLAUDE.md, docs/, config/ e .claude/agents/.

Não execute pesquisa nem altere arquivos.

Confirme:
1. Quais subagentes foram encontrados, com nome, caminho e finalidade.
2. Se cada arquivo possui frontmatter reconhecível pelo ambiente atual.
3. Se há arquivos, regras ou configurações ausentes.
4. A ordem correta de delegação do orquestrador.
5. Quais dados ainda precisam ser fornecidos manualmente antes da primeira rodada real.

Se encontrar problemas, apresente apenas um plano de correção e patches sugeridos. Aguarde minha aprovação antes de editar qualquer arquivo.
Prompt para rodada piloto
text
Execute uma rodada piloto do Radar de Editais — Dhara / IFA Records.

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

Entregue relatório diário em português do Brasil, com oportunidades urgentes, prioritárias, pendências e recomendações de próxima ação.
Relatórios e alertas
Alerta urgente
Gerar alerta URGENTE quando:

A oportunidade estiver aberta e validada.

A decisão for APLICAR ou AVALIAR_COM_PARCERIA.

O prazo final estiver em até sete dias.

Alta prioridade
Marcar ALTA PRIORIDADE quando:

O score for igual ou superior a 75.

O status aberto estiver confirmado.

O nível de confiança for igual ou superior a 0,70.

Relatório diário
Deve incluir:

Urgentes.

Novas oportunidades prioritárias.

Alterações em prazo, status ou regulamento.

Casos que exigem revisão humana.

Fontes consultadas, falhas e limitações.

Próximas ações recomendadas.

Relatório semanal
Deve incluir:

Pipeline por status e decisão.

Ranking das 10 oportunidades mais relevantes.

Calendário de prazos dos próximos 30 dias.

Checklist documental consolidado.

Blocos separados para oportunidades nacionais e internacionais.

Padrões identificados e melhorias sugeridas para o kit de inscrição.

Segurança e governança
Não enviar inscrições, e-mails, mensagens, documentos, declarações ou formulários sem autorização humana explícita.

Não realizar pagamentos, compras, contratações, assinaturas ou compromissos em nome da IFA ou da Dhara.

Não registrar tokens, senhas, certificados, documentos societários, dados bancários ou dados pessoais sensíveis em arquivos versionados.

Usar variáveis de ambiente para credenciais, quando uma integração aprovada exigir isso.

Respeitar termos de uso, robots.txt, limites de requisição, copyright e regras de acesso das fontes.

Não tentar burlar CAPTCHA, autenticação, paywalls, anti-bot ou bloqueios técnicos.

Tratar a saída do agente como recomendação assistida: a decisão final de aplicação é humana.

Manutenção recomendada
Frequência	Atividade
Frequência	Atividade
Diária, em dias úteis	Rodada de descoberta, validação, score e alertas.
Semanal	Revisão de pipeline, prazos, parcerias e decisões de candidatura.
Mensal	Atualização das fontes, pesos do score e kit documental.
A cada edital prioritário	Criar uma pasta/dossiê de candidatura, checklist e versão adaptada do projeto.
A cada alteração estrutural	Revisar CLAUDE.md, agentes e documentos de contexto.
Estado atual do projeto
O repositório começa como uma camada de instruções e operação assistida pelo Claude. Ele pode evoluir futuramente para integrar bases estruturadas, automações de coleta, banco de dados e APIs, desde que sejam preservadas estas regras:

validação em fonte oficial;

evidência auditável;

revisão humana para decisões críticas;

cobertura nacional e internacional;

avaliação correta da IFA Sounds como PJ no Simples Nacional.
