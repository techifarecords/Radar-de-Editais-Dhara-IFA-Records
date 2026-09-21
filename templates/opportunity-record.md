---
# Modelo de registro de oportunidade.
# Gravar em: data/validated/AAAA-MM-DD-{{slug-da-oportunidade}}.md
# Mover para data/archive/ quando o status do funil for ENCERRADO, DESCARTADO,
# APROVADO ou NAO_APROVADO. Gravação só com pedido explícito da pessoa usuária.
# Campos não localizados: usar null e listar em campos_nao_localizados.

id: "{{slug}}"
titulo_oficial: ""
identificador: null
instituicao: ""
tipo: ""                  # edital | prêmio | residência | festival | showcase | contratação | intercâmbio | outro
linguagem: []
modalidade: ""

territorio:
  pais: null
  estado_regiao: null
  cidade: null
  abrangencia: null       # municipal | estadual | nacional | internacional
  territorio_execucao: []
  territorio_proponente: []

links:
  url_descoberta: ""
  url_oficial: ""
  url_inscricao: ""
  url_regulamento: ""
  retificacoes: []

fonte:
  fonte_descoberta: ""    # oficial | PROSAS | parceiro | mídia | newsletter | rede social
  fonte_oficial_confirmada: false

prazos:
  status_validado: DESCONHECIDA     # original: ANUNCIADA | ABERTA | ENCERRADA | SUSPENSA | PRORROGADA | DESCONHECIDA
  status_operacional: DESCONHECIDA  # usado em decisões e alertas; PRORROGADA confirmada => ABERTA
  prorrogacao:
    data_hora: null
    url: null
    evidencia: null
  data_publicacao: null
  abertura: null
  encerramento: null
  timezone: null
  texto_original_do_prazo: null

recursos:
  valor_maximo: null
  valor_minimo: null
  orcamento_total: null
  moeda: null
  numero_selecionados: null
  itens_financiaveis: []
  itens_vedados: []

elegibilidade:
  proponentes_aceitos: []   # PF | PJ | MEI | coletivo | associação | outro
  requisitos_pj: []
  requisitos_artista: []
  exige_parceiro_local: null
  documentos: []
  contrapartidas: []
  criterios_avaliacao: []
  restricoes: []

analise:
  score_total: null
  subpontuacoes:
    aderencia_artistica: null
    formato_escopo: null
    elegibilidade: null
    territorio_internacionalizacao: null
    viabilidade_financeira: null
    janela_operacional: null
    confiabilidade: null
    valor_estrategico: null
  penalidades: []
  decisao: null           # APLICAR | AVALIAR_COM_PARCERIA | MONITORAR | DESCARTAR
  prioridades: []         # URGENTE | ALTA_PRIORIDADE | REVISAO
  confidence_score: null
  riscos: []
  pendencias: []
  proxima_acao: ""

pipeline:
  status_funil: DESCOBERTO   # valores sem acento; ver docs/04_PIPELINE_E_STATUS.md
  responsavel: null          # somente humano; nunca preenchido pelo radar
  human_review_required: true

notion:                      # ver docs/07_NOTION_OPERACAO.md
  chave_deduplicacao: null   # URL canônica | id:<instituicao>:<identificador> | descoberta:<url>
  page_id: null              # preenchido após criação aprovada
  sincronizavel: false       # true somente com decisão APLICAR, AVALIAR_COM_PARCERIA ou MONITORAR
  ultima_sincronizacao: null # AAAA-MM-DD HH:MM (fuso)
  status_sincronizacao: null # criado | atualizado | pendente | aguardando_aprovacao_estrategica | recusado | adiado | bloqueado | falhou | possivel_duplicata
  propostas_estrategicas: []  # {campo, valor_atual, valor_proposto, motivo, url, data_hora, resposta}

campos_nao_localizados: []
conflitos_de_fonte: []
ultima_validacao: null     # AAAA-MM-DD HH:MM (fuso)
---

# {{Título oficial}}

## Resumo

{{Duas ou três frases sobre a oportunidade e a aderência à Dhara / IFA.}}

## Evidências

| Afirmação | Trecho da fonte | URL | Data/hora da coleta |
|---|---|---|---|
| {{status / prazo / regra crítica}} | {{trecho curto}} | {{url}} | {{AAAA-MM-DD HH:MM}} |

## Justificativa do score

{{Explicação por dimensão e penalidades aplicadas, conforme o dhara-fit-scorer.}}

## Checklist inicial

- [ ] {{item}}

## Notas

{{Observações humanas.}}

## Histórico de alterações

Preservar mudanças de prazo, status, regulamento e valor. Não sobrescrever evidências anteriores. No Notion, cada linha nova é acrescentada ao fim da seção "Histórico de alterações" da página, nunca editada.

- {{AAAA-MM-DD HH:MM}} ({{fuso}}) — {{evento}}. Fonte: {{url}}. Trecho: "{{trecho}}".
	- {{campo}}: {{antes}} → {{depois}}
