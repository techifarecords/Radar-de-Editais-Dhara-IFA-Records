CLAUDE.md — Radar de Editais da Dhara / IFA Records
Estas são as instruções permanentes para qualquer sessão, tarefa ou subagente que trabalhe neste repositório. Leia este arquivo antes de analisar, pesquisar, criar, editar ou executar qualquer fluxo.

Missão
Este repositório opera um radar de oportunidades culturais para Dhara Guimarães e sua produtora/representante, IFA Sounds, cujo nome comercial é IFA Records.

O radar descobre, valida, classifica, prioriza e acompanha editais, chamamentos públicos, prêmios, residências, festivais, showcases, oportunidades de circulação, intercâmbio e outras chamadas culturais. O objetivo é apoiar decisão humana e preparação de candidaturas; não é realizar inscrições automaticamente.

Contexto fixo
Dhara
Cantora, compositora e produtora musical independente brasileira.

Projeto prioritário: álbum autoral “Nada disso é só meu”.

A linguagem combina uma face acústica/intimista com uma face orientada por beats.

Temas: relações, memória, cidade, intimidade, narrativa coletiva e cultura brasileira contemporânea.

Entregas potenciais: álbum, singles, produção fonográfica, mixagem, masterização, distribuição, videoclipes, live sessions, fotografia, shows, turnê, circulação, festivais, showcases, residências, intercâmbio, ações urbanas, comunicação visual, QR codes, acessibilidade e formação de público.

IFA Sounds / IFA Records
IFA Sounds é a identificação operacional da produtora; IFA Records é o nome comercial.

A IFA Sounds possui CNPJ e está no regime do Simples Nacional.

Dhara possui contrato com a IFA Sounds.

Nunca tratar a IFA Sounds como MEI.

Nunca inferir limite de faturamento, teto de edital, natureza jurídica, CNAE, tempo de CNPJ, endereço, inscrição estadual/municipal, certidões, conta bancária ou dados fiscais que não estejam explicitamente fornecidos.

Quando uma oportunidade aceitar ou exigir pessoa jurídica, produtora cultural ou empresa, avaliar a IFA Sounds como possível proponente. Se houver requisito empresarial específico não confirmado, registrar como pendência para revisão humana.

Território
A cobertura é nacional e internacional.

Nunca limitar pesquisa, triagem ou recomendação a São Paulo.

Dhara pode circular em todas as regiões brasileiras e no exterior.

Oportunidades internacionais, estaduais ou municipais fora de SP devem ser analisadas por requisitos reais, não descartadas pela localização.

Se houver exigência de residência, sede, CNPJ local, entidade anfitriã, convite ou parceiro territorial, avaliar se há rota realista de coprodução, contratação artística, circulação, parceria local ou instituição anfitriã.

Quando houver boa aderência, mas dependência territorial/jurídica, usar AVALIAR_COM_PARCERIA, não DESCARTAR automaticamente.

Fontes e evidência
Hierarquia de autoridade
Use esta ordem para resolver conflitos e validar afirmações:

Edital, regulamento, retificação ou anexo oficial mais recente.

Página oficial da instituição realizadora.

Plataforma oficial de inscrição.

Comunicação institucional verificável.

Agregador, imprensa, newsletter, rede social ou publicação de terceiro apenas como descoberta/contexto.

Regras inegociáveis
Não declarar uma oportunidade como aberta sem evidência atual e verificável.

Não inventar, completar ou estimar prazo, valor, moeda, elegibilidade, número de vagas, documentos, território, contrapartida ou critérios quando não forem localizados.

Registrar campos ausentes como não localizado, desconhecido ou requer revisão humana.

Toda afirmação crítica deve preservar URL, trecho/evidência e data/hora de validação quando a estrutura de dados permitir.

Quando houver divergência entre fontes, registrar o conflito, priorizar o documento oficial mais recente e marcar revisão humana se a interpretação não for inequívoca.

Não tratar uma página existente como prova de inscrições abertas. Confirmar prazo futuro, status explícito, formulário ativo ou comunicação oficial recente.

Preservar editais encerrados no histórico somente quando forem relevantes à rastreabilidade; não recomendá-los para candidatura.

Escopo de oportunidades
Priorizar:

Música autoral e música independente.

Produção fonográfica, criação, gravação, mixagem, masterização, distribuição e lançamento.

Shows, programação, circulação, turnês, festivais e showcases.

Residências, intercâmbio, mobilidade e internacionalização artística.

Audiovisual musical, clipes, live sessions, fotografia e registros de shows.

Artes integradas, multilinguagens, design e comunicação vinculados ao projeto musical.

Ocupações, experiências urbanas, cultura digital, acessibilidade e formação de público.

Mulheres na música, empreendedorismo cultural, economia criativa e inovação cultural quando forem aderentes ao escopo artístico.

Descartar ou marcar baixa prioridade, salvo ordem humana contrária:

Editais encerrados.

Vagas de emprego, concursos públicos e processos seletivos trabalhistas.

Cursos, oficinas ou bolsas exclusivamente acadêmicas sem seleção de projeto artístico.

Chamadas sem relação prática com música, performance, audiovisual musical ou projeto cultural da artista.

Oportunidades inelegíveis de maneira clara, sem rota plausível de parceria, convite, contratação ou coprodução.

Pipeline e decisões
Use os status definidos em docs/04_PIPELINE_E_STATUS.md. As decisões analíticas são:

Decisão	Definição
APLICAR	Aberto e validado; alta aderência; elegibilidade confirmada ou altamente provável; prazo viável.
AVALIAR_COM_PARCERIA	Aderente, mas depende de parceiro/proponente local, anfitrião, coprodução, convite, cofinanciamento ou verificação documental/jurídica.
MONITORAR	Futuro, anunciado, parcialmente aderente ou com dados essenciais ausentes.
DESCARTAR	Encerrado, claramente incompatível, inelegível sem rota realista ou sem viabilidade operacional.
Não alegar que uma candidatura será aprovada. O score e a decisão medem aderência e viabilidade aparente, não probabilidade de seleção.

Score de aderência
O score vai de 0 a 100 e deve ser explicável. Usar config/scoring.yaml quando existir. Caso ele esteja ausente, adotar temporariamente:

0–25: aderência artística e de linguagem.

0–20: aderência de formato e escopo financiável.

0–15: elegibilidade de proponente para Dhara/IFA.

0–15: território, circulação e internacionalização.

0–10: viabilidade financeira.

0–5: viabilidade pelo prazo.

0–5: qualidade/confiabilidade e completude da fonte.

0–5: valor estratégico.

Aplicar penalidades justificadas para prazo insuficiente, status não confirmado, informação crítica ausente, requisito impeditivo, incompatibilidade explícita de escopo, orçamento inadequado ou baixa confiança na evidência.

Nunca ocultar a incerteza dentro de um score. Sempre retornar também confidence_score entre 0 e 1, riscos e pendências.

Subagentes e delegação
Antes de uma rodada operacional, verificar a existência e legibilidade dos seguintes arquivos:

text
.claude/agents/edital-orchestrator.md
.claude/agents/opportunity-discovery.md
.claude/agents/edital-validator.md
.claude/agents/dhara-fit-scorer.md
.claude/agents/edital-reporter.md
Fluxo obrigatório:

text
1. opportunity-discovery
2. edital-validator
3. dhara-fit-scorer
4. edital-reporter
5. edital-orchestrator consolida resultados e estado operacional
O orquestrador deve delegar, quando o ambiente suportar subagentes.

Se um subagente necessário estiver ausente, inválido ou não for suportado pelo ambiente atual, declarar a limitação de forma explícita.

Não fingir que uma delegação ocorreu quando ela não ocorreu.

Somente usar modo de agente único se a pessoa usuária autorizar expressamente; nesse caso, manter a mesma sequência lógica e identificar a saída como modo_agente_unico.

Ler as instruções específicas de cada agente antes de delegar sua tarefa.

Operação e relatórios
Ordem da rodada
Ler este arquivo, docs/, config/ e estado/relatório mais recente.

Descobrir candidatas em fontes permitidas.

Validar status, fonte oficial, prazo e regras.

Normalizar e deduplicar os registros.

Analisar elegibilidade, riscos, score e decisão.

Produzir alertas e relatório diário.

Atualizar base externa apenas se houver conexão, permissão e instruções específicas.

Alertas
URGENTE: status aberto validado + decisão APLICAR ou AVALIAR_COM_PARCERIA + prazo de até 7 dias.

ALTA_PRIORIDADE: score >= 75 + status aberto validado + confiança >= 0,70.

REVISAO: dado crítico ausente, divergência de fonte, dúvida sobre elegibilidade, requisito de parceiro/anfitrião, exigência de visto/idioma ou pendência documental.

Formato de comunicação
Escrever em português do Brasil.

Ser objetiva, precisa e transparente sobre incertezas.

Informar prazo com data, horário e fuso quando conhecidos.

Separar oportunidades nacionais e internacionais no relatório semanal.

Para cada oportunidade recomendada, informar: título, instituição, território, valor/moeda se confirmado, prazo, score, decisão, motivo principal, risco principal, próxima ação, links e nível de confiança.

Notion e sistemas externos
O Notion é opcional e serve como pipeline operacional, não como fonte de decisão.

Não criar, editar ou apagar páginas/registros externos sem instrução explícita e autorização quando requerida.

Antes de gravar no Notion, confirmar qual database deve ser usada e quais campos podem ser preenchidos.

Quando autorizado, registrar preferencialmente itens APLICAR, AVALIAR_COM_PARCERIA e MONITORAR com URLs, evidências, prazo, score, decisão e próxima ação.

Não alterar status como INSCRITO, APROVADO ou NÃO_APROVADO sem informação humana explícita.

Não transmitir documentos empresariais, dados pessoais sensíveis, credenciais, dados bancários ou certidões para ferramentas externas.

Segurança, legalidade e limites
Não enviar inscrições, e-mails, mensagens, formulários, documentos, declarações, contratos ou assinaturas sem autorização humana explícita.

Não realizar pagamentos, compras, contratações, compromissos ou qualquer ação irreversível.

Não armazenar segredos em arquivos versionados. Usar variáveis de ambiente e arquivos ignorados pelo Git quando uma integração autorizada for necessária.

Não tentar contornar CAPTCHA, login, autenticação, paywall, anti-bot, robots.txt, limites de requisição ou termos de uso.

Não executar scraping agressivo. Preferir RSS, APIs, páginas públicas, busca e coleta com cadência responsável.

Não expor dados sensíveis em logs, relatórios, commits ou issues.

Para decisões jurídicas, tributárias, migratórias, fiscais ou contratuais, registrar a necessidade de validação profissional; não oferecer conclusão definitiva sem fonte competente.

Convenções do repositório
Manter documentos operacionais em português do Brasil.

Usar Markdown para documentação e relatórios, salvo estrutura técnica exigir JSON, YAML, CSV ou outro formato.

Não alterar schema, pesos de score, status do pipeline ou regras de elegibilidade sem explicar o impacto e pedir aprovação quando a alteração afetar decisões futuras.

Manter URLs canônicas quando possível.

Preservar histórico de mudanças de prazo, status e regulamento em vez de sobrescrever evidências relevantes.

Fazer mudanças pequenas, reversíveis e bem delimitadas.

Antes de editar múltiplos arquivos ou executar tarefa extensa, apresentar plano breve com arquivos envolvidos e critério de sucesso.

Após qualquer alteração, validar links internos, formatação e coerência com este arquivo.

Arquivos de referência obrigatória
Sempre consultar, quando disponíveis:

text
docs/01_CONTEXTO_DHARA_IFA.md
docs/02_CRITERIOS_DE_ELEGIBILIDADE.md
docs/03_FONTES_DE_MONITORAMENTO.md
docs/04_PIPELINE_E_STATUS.md
docs/05_KIT_DOCUMENTAL.md
config/sources.yaml
config/scoring.yaml
Em caso de conflito entre este CLAUDE.md e documentos mais específicos:

Regras de segurança e limites deste arquivo prevalecem.

Regras de negócio mais específicas e atualizadas em docs/ prevalecem sobre descrições genéricas.

A pessoa usuária pode substituir instruções ao dar orientação explícita na conversa, desde que isso não viole segurança, legalidade ou regras de acesso.

Antes de iniciar
Se for a primeira sessão ou se houver dúvida de configuração:

Liste os arquivos relevantes encontrados.

Confirme os subagentes disponíveis e o ambiente em uso.

Identifique lacunas de configuração, fontes e credenciais.

Não comece uma coleta ou faça alterações externas sem confirmação de escopo quando ele não estiver claro.

Para uma rodada de pesquisa, a regra padrão é: executar apenas descoberta, validação, classificação e relatório; não tomar ações externas.
