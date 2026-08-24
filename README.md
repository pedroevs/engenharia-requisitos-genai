# Sistema de Gestão de Eventos — Engenharia de Requisitos com IA Generativa

## Descrição

Este projeto foi desenvolvido como atividade prática da disciplina de Engenharia de Requisitos. O objetivo é analisar o documento de elicitação de requisitos de um Sistema de Gestão de Eventos (empresa Eventus) e produzir artefatos de especificação utilizando Inteligência Artificial Generativa como ferramenta de apoio.

## Contexto do Projeto

A empresa Eventus organiza congressos, workshops e eventos corporativos. Atualmente, o gerenciamento de inscrições é realizado por meio de formulários on-line e planilhas eletrônicas, dificultando o controle de vagas, pagamentos, cancelamentos e emissão de certificados. O projeto visa centralizar essas atividades em um sistema único.

## Estrutura do Repositório

engenharia-requisitos-genai/
├── README.md
├── analise/
│   ├── requisitos-funcionais.md
│   ├── requisitos-nao-funcionais.md
│   ├── regras-de-negocio.md
│   └── duvidas-e-lacunas.md
└── especificacao/
    ├── historias-usuario.md
    ├── casos-de-uso.md
    └── criterios-aceitacao.md

## Artefatos Produzidos

- Análise de Requisitos Funcionais (14 requisitos)
- Análise de Requisitos Não Funcionais (7 requisitos)
- Regras de Negócio (9 regras)
- Dúvidas e Lacunas identificadas (10 pontos)
- Histórias de Usuário (11 histórias)
- Casos de Uso (5 casos com fluxos detalhados)
- Critérios de Aceitação (para cada história)

## Ferramentas Utilizadas

- Visual Studio Code
- Git e GitHub
- Markdown
- IA Generativa (Adapta ONE) como ferramenta de apoio

## Reflexão sobre o uso de IA Generativa

### Como a IA apoiou o processo

1. **Análise do documento de elicitação:** A IA auxiliou na leitura crítica, identificando requisitos funcionais implícitos nas falas dos stakeholders, distinguindo requisitos de regras de negócio e sinalizando lacunas e ambiguidades.

2. **Seleção de artefatos:** A IA foi consultada sobre quais artefatos seriam mais adequados. Sugestões como diagramas de classe, BPMN e protótipos foram avaliadas, mas histódrias de usuário, casos de uso e critérios de aceitação foram considerados suficientes e mais alinhados ao escopo.

3. **Elaboração e refinamento:** A IA auxiliou na redação inicial das histórias, na estruturação dos fluxos dos casos de uso e na formulação dos critérios de aceitação. O engenheiro de requisitos revisou, ajustou e validou todos os artefatos.

### Sugestões: aproveitadas, modificadas e descartadas

**Aproveitadas:**
- Agrupar histórias de usuário por ator (facilita rastreabilidade)
- Criar arquivo separado para regras de negócio
- Incluir critérios de aceitação estruturados para histórias complexas

**Modificadas:**
- 12 histórias sugeridas pela IA → consolidadas em 11 (inscrição e comprovante unificados)
- Diagramas de sequência UML sugeridos → substituídos por casos de uso com fluxos detalhados
- Critérios de aceitação ajustados para incluir regras de negócio específicas (lista de espera, reembolso condicional)

**Descartadas:**
- Protótipos de tela — fora do escopo de especificação de requisitos
- Diagrama ER — artefato de design, não de requisitos
- Glossário de termos — domínio de fácil compreensão
