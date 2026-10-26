# Testes de Integração com IA Generativa — Sistema de Gestão de Eventos
 
## Descrição
Atividade prática da disciplina de Ferramentas de IA Generativa aplicadas à Engenharia de Software (Unidade III). O objetivo é experimentar diferentes tipos de prompt (zero-shot, few-shot e chain-of-thought) para apoiar a geração de casos de teste de integração entre serviços REST de um Sistema de Gestão de Eventos (empresa Eventus).
 
## Cenário de integração
- Serviço de Inscrições (API REST)
- Serviço de Pagamentos (API REST)
- Serviço de Notificações (API REST)
 
## Estrutura
testes-integracao/
├── README.md
├── prompts/
│   ├── prompt-1-zero-shot-openapi.md
│   ├── prompt-2-few-shot-exemplos.md
│   └── prompt-3-chain-of-thought.md
└── casos-de-teste/
    ├── casos-de-teste-integracao.md
    └── analise-ajustes-prompts.md
 
## Reflexão
Os três tipos de prompt produziram resultados complementares: o zero-shot com contrato OpenAPI garantiu aderência técnica; o few-shot trouxe consistência de formato e cobertura de casos de erro; o chain-of-thought revelou pontos de falha (timeout, contrato inválido, concorrência) que não apareciam nos demais.
