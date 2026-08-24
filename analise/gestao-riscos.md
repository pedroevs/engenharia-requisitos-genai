# Gestão de Riscos do Projeto — Sistema de Gestão de Eventos

## 1. Metodologia

A gestão de riscos foi conduzida com base no guia PMBOK (PMI), utilizando análise quali-quantitativa de probabilidade e impacto. Os riscos foram identificados a partir da análise dos requisitos funcionais e não funcionais, das regras de negócio e das lacunas identificadas durante a fase de elicitação.

### Matriz de Avaliação

| Nível | Probabilidade | Impacto | Classificação |
|-------|--------------|---------|---------------|
| 1 | Muito Baixa | Insignificante | Baixo |
| 2 | Baixa | Menor | Baixo |
| 3 | Média | Moderado | Médio |
| 4 | Alta | Maior | Alto |
| 5 | Muito Alta | Crítico | Crítico |

### Critérios de Impacto

- **Insignificante:** Sem efeito no projeto
- **Menor:** Pequeno atraso, sem impacto no escopo
- **Moderado:** Atraso visível, requer ajustes no cronograma
- **Maior:** Impacto significativo em custo, prazo ou escopo
- **Crítico:** Pode comprometer a viabilidade do projeto

---

## 2. Registro de Riscos

### Riscos Técnicos

## R01 — Falha de Integração com Gateway de Pagamento

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Técnico |
| **Descrição** | O gateway de pagamento terceirizado pode apresentar instabilidade ou indisponibilidade durante o processo de inscrição em eventos pagos, impedindo a confirmação de pagamento. |
| **Probabilidade** | 3 (Média) |
| **Impacto** | 4 (Maior) |
| **Nível de Risco** | ALTO (12) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Implementar mecanismo de retentativa automática com backoff exponencial; provisionar fallback para pagamento via PIX manual; monitorar disponibilidade do gateway com alertas em tempo real. |
| **Plano de Contingência** | Acionar fluxo manual de confirmação de pagamento pela equipe financeira; notificar participantes sobre possível atraso na confirmação. |
| **Responsável** | Equipe de TI |

## R02 — Indisponibilidade do Sistema em Período de Pico

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Técnico |
| **Descrição** | Durante a abertura de inscrições de eventos de grande porte, o sistema pode não suportar picos de acesso simultâneo, degradando性能 ou ficando indisponível. |
| **Probabilidade** | 4 (Alta) |
| **Impacto** | 5 (Crítico) |
| **Nível de Risco** | CRÍTICO (20) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Implementar arquitetura escalável com auto-scaling; realizar testes de carga simulando 500+ usuários simultâneos (conforme RNF06); configurar rate limiting e filas de processamento. |
| **Plano de Contingência** | Ativar modo degradado com apenas funcionalidades essenciais (consulta e inscrição); exibir mensagem de fila virtual aos usuários. |
| **Responsável** | Equipe de TI |

## R03 — Inconsistência no Controle de Vagas por Concorrência

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Técnico |
| **Descrição** | Múltiplas inscrições simultâneas em um evento com vagas limitadas podem gerar race condition, resultando em mais inscrições do que vagas disponíveis. |
| **Probabilidade** | 3 (Média) |
| **Impacto** | 4 (Maior) |
| **Nível de Risco** | ALTO (12) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Implementar locking otimista ou pessimista no controle de vagas; usar transações atômicas no banco de dados; validar disponibilidade de vagas em tempo real antes de confirmar cada inscrição. |
| **Plano de Contingência** | Identificar inscrições excedentes e oferecer lista de espera automática aos usuários afetados. |
| **Responsável** | Equipe de TI |

### Riscos de Segurança e Privacidade

## R04 — Vazamento de Dados Pessoais de Participantes (LGPD)

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Segurança / Legal |
| **Descrição** | Dados sensíveis de participantes (documentos, informações financeiras) podem ser expostos por falha de segurança, invasão externa ou acesso indevido por usuários internos, resultando em violação da LGPD. |
| **Probabilidade** | 2 (Baixa) |
| **Impacto** | 5 (Crítico) |
| **Nível de Risco** | ALTO (10) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Criptografar dados sensíveis em repouso e em trânsito; implementar controle de acesso baseado em perfis (RBAC); restringir acesso de palestrantes a dados mínimos (RN08); realizar auditorias de segurança periódicas; treinar equipe sobre LGPD. |
| **Plano de Contingência** | Acionar plano de resposta a incidentes; notificar ANPD em até 3 dias úteis; comunicar participantes afetados conforme exigência legal. |
| **Responsável** | Equipe de TI / DPO |

## R05 — Emissão Fraudulenta de Certificados

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Segurança |
| **Descrição** | Usuários não participantes podem acessar o sistema e emitir certificados de eventos que não frequentaram, ou participantes podem burlar a confirmação de presença. |
| **Probabilidade** | 3 (Média) |
| **Impacto** | 3 (Moderado) |
| **Nível de Risco** | MÉDIO (9) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Implementar validação de presença via QR Code nos eventos que exigem confirmação; gerar certificados com assinatura digital e código de verificação público; registrar logs auditáveis de todas as emissões (RNF07). |
| **Plano de Contingência** | Invalidar certificados fraudulentos identificados; acionar medidas legais se necessário. |
| **Responsável** | Organizador / Equipe de TI |

### Riscos de Negócio

## R06 — Ambiguidade nas Regras de Cancelamento e Reembolso

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Negócio / Requisitos |
| **Descrição** | As lacunas identificadas (L01, L02) sobre prazos de cancelamento e condições de reembolso podem gerar disputas com participantes, insatisfação e prejuízo financeiro se as regras não forem claramente definidas e comunicadas. |
| **Probabilidade** | 4 (Alta) |
| **Impacto** | 3 (Moderado) |
| **Nível de Risco** | ALTO (12) |
| **Estratégia** | Evitar |
| **Ações Preventivas** | Definir e documentar políticas de cancelamento e reembolso antes do desenvolvimento; exibir as regras de forma transparente ao participante antes da confirmação da inscrição; obter aceite explícito dos termos. |
| **Plano de Contingência** | Provisão de contingência financeira para reembolsos improváveis; canal dedicado de atendimento para disputas. |
| **Responsável** | Organizador / Equipe Financeira |

## R07 — Resistência à Adoção por Parte dos Organizadores

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Negócio / Pessoas |
| **Descrição** | Os organizadores, acostumados com planilhas e formulários, podem resistir à adoção do novo sistema, comprometendo o ROI do projeto e a qualidade dos dados. |
| **Probabilidade** | 3 (Média) |
| **Impacto** | 3 (Moderado) |
| **Nível de Risco** | MÉDIO (9) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Envolvimento dos organizadores desde a fase de elicitação; treinamento prático antes do lançamento; interface intuitiva focada na experiência do usuário; sessões de feedback contínuo. |
| **Plano de Contingência** | Período de transição com operação paralela (sistema + planilhas); suporte dedicado nos primeiros eventos. |
| **Responsável** | Gestão de Projetos |

## R08 — Falha no Envio de Notificações

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Técnico / Operacional |
| **Descrição** | O sistema pode falhar no envio de comprovantes de inscrição, notificações de pagamento e alertas de lista de espera (RF12), gerando reclamações e perda de confiança dos participantes. |
| **Probabilidade** | 3 (Média) |
| **Impacto** | 3 (Moderado) |
| **Nível de Risco** | MÉDIO (9) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Utilizar serviço de e-mail transacional com garantia de entrega; implementar fila de mensagens com retentativa automática; disponibilizar comprovantes e notificações também dentro do sistema (autoatendimento). |
| **Plano de Contingência** | Envio manual de comprovantes críticos; status visível no sistema para consulta alternativa. |
| **Responsável** | Equipe de TI |

### Riscos de Cronograma e Escopo

## R09 — Estouro de Escopo por Requisitos Não Elicitados

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Projeto / Escopo |
| **Descrição** | As 10 lacunas identificadas na fase de elicitação (L01 a L10) podem gerar novos requisitos durante o desenvolvimento, causando estouro de prazo e custo. |
| **Probabilidade** | 4 (Alta) |
| **Impacto** | 3 (Moderado) |
| **Nível de Risco** | ALTO (12) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Conduzir rodada suplementar de elicitação para esclarecer as lacunas antes do desenvolvimento; priorizar requisitos essenciais (MVP) e diferir melhorias para versões futuras; gerenciar mudanças via controle formal de escopo. |
| **Plano de Contingência** | Avaliar impacto de cada nova demanda e negociar prazos/custo com os stakeholders. |
| **Responsável** | Gestão de Projetos |

## R10 — Dependência de Decisões de Stakeholders Não Disponíveis

| Atributo | Descrição |
|----------|-----------|
| **Categoria** | Projeto / Comunicação |
| **Descrição** | Decisões sobre lacunas (ex: política de reembolso, emissão de certificados, dados visíveis a palestrantes) dependem de stakeholders que podem não estar disponíveis em tempo hábil, bloqueando o desenvolvimento. |
| **Probabilidade** | 3 (Média) |
| **Impacto** | 3 (Moderado) |
| **Nível de Risco** | MÉDIO (9) |
| **Estratégia** | Mitigação |
| **Ações Preventivas** | Agendar reuniões de validação com todos os stakeholders no início do projeto; definir prazos para tomada de decisão; estabelecer um comitê de decisão com poder deliberativo para casos de ausência. |
| **Plano de Contingência** | Adotar soluções provisórias com registro técnico de débito (technical debt) para revisão posterior. |
| **Responsável** | Gestão de Projetos |

---

## 3. Resumo da Matriz de Riscos

| ID | Risco | Prob. | Impacto | Nível | Estratégia |
|----|-------|-------|---------|-------|------------|
| R02 | Indisponibilidade em pico | 4 | 5 | CRÍTICO | Mitigação |
| R01 | Falha no gateway de pagamento | 3 | 4 | ALTO | Mitigação |
| R03 | Concorrência no controle de vagas | 3 | 4 | ALTO | Mitigação |
| R04 | Vazamento de dados (LGPD) | 2 | 5 | ALTO | Mitigação |
| R06 | Ambiguidade em cancelamento/reembolso | 4 | 3 | ALTO | Evitar |
| R09 | Estouro de escopo | 4 | 3 | ALTO | Mitigação |
| R05 | Emissão fraudulenta de certificados | 3 | 3 | MÉDIO | Mitigação |
| R07 | Resistência à adoção | 3 | 3 | MÉDIO | Mitigação |
| R08 | Falha em notificações | 3 | 3 | MÉDIO | Mitigação |
| R10 | Dependência de stakeholders | 3 | 3 | MÉDIO | Mitigação |

---

## 4. Estratégia de Resposta Prioritária

**R02 — Indisponibilidade do Sistema em Período de Pico** é considerado o risco de maior criticidade (nível CRÍTICO). A estratégia de mitigação envolve:

1. **Arquitetura escalável:** Auto-scaling horizontal para suportar picos de 500+ usuários simultâneos (RNF06)
2. **Testes de carga:** Simulação de cenários de pico antes de cada evento de grande porte
3. **Modo degradado:** Funcionalidades não essenciais (consulta de histórico, emissão antecipada de certificados) são temporariamente desativadas para preservar as operações críticas (inscrição e pagamento)
4. **Monitoramento proativo:** Dashboards em tempo real com alertas automáticos de CPU, memória e latência

Esta estratégia é prioritária porque um único evento de indisponibilidade durante um período de inscrições de alto volume pode comprometer a reputação do sistema, gerar perda de receita e tensionar o relacionamento com os organizadores.
