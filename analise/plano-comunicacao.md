# Plano de Comunicação — Gestão de Riscos

## 1. Objetivo

 Este plano define os canais, frequências, formatos e responsabilidades de comunicação entre os stakeholders do projeto do Sistema de Gestão de Eventos, com foco na gestão de riscos e na comunicação de incidentes.

---

## 2. Stakeholders e Necessidades de Comunicação

| Stakeholder | Interesse na Comunicação | Canal Preferencial |
|-------------|--------------------------|-------------------|
| Organizadores | Status do projeto, riscos de negócio, impacto em eventos | E-mail + Reuniões |
| Equipe Financeira | Riscos de pagamento, reembolso, status financeiro | E-mail + Dashboard |
| Equipe de TI | Riscos técnicos, incidentes, performance | Slack + Dashboard |
| Participantes | Avisos de indisponibilidade, atrasos em inscrições | E-mail + Sistema |
| Palestrantes | Alterações em programação, acesso ao sistema | E-mail |
| Gestão de Projetos | Visão consolidada, decisões pendentes | Dashboard + Reuniões |

---

## 3. Matriz de Comunicação de Rotina

| Comunicação | Frequentcia | Formato | Responsável | Destinatários |
|-------------|------------|---------|-------------|----------------|
| Status do projeto | Semanal | Relatório resumido | Gestor de Projetos | Organizadores, Equipe de TI |
| Revisão de riscos | Quinzenal | Reunião (30 min) | Gestor de Projetos | Stakeholders principais |
| Métricas técnicas | Diária | Dashboard automático | Equipe de TI | Gestor de Projetos |
| Pendências (lacunas) | Por reunião | Documento compartilhado | Gestor de Projetos | Stakeholders responsáveis |
| Status de desenvolvimento | Semanal | Demonstração (demo) | Equipe de TI | Organizadores |

---

## 4. Plano de Comunicação de Incidentes

### Classificação de Incidentes

| Nível | Descrição | Tempo de Notificação | Escalação |
|-------|-----------|-----------------------|-----------|
| P0 — Crítico | Sistema indisponível, vazamento de dados | Imediato (até 15 min) | Gestor de Projetos + Equipe de TI + Organizadores |
| P1 — Alto | Funcionalidade crítica com falha (inscrição, pagamento) | Até 30 min | Equipe de TI + Gestor de Projetos |
| P2 — Médio | Funcionalidade degradada, impacto parcial | Até 2h | Equipe de TI + Gestor de Projetos |
| P3 — Baixo | Issues não críticos, sem impacto imediato | Próxima revisão | Equipe de TI |

### Fluxo de Comunicação de Incidente P0/P1

1. **Detecção** → Equipe de TI identifica (ou recebe alerta automático)
2. **Notificação interna** → Mensagem no canal Slack de incidentes (até 15 min)
3. **Avaliação** → Classificação do nível e impacto (até 30 min)
4. **Comunicação a stakeholders** → E-mail com descrição, impacto estimado e prazo de resolução (até 1h)
5. **Atualizações** → A cada 2h ou a cada mudança de status
6. **Resolução** → Confirmação de normalização + relatório pós-incidente (até 48h)

### Template de Notificação de Incidente
