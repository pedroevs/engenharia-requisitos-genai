# Requisitos Não Funcionais

## RNF01 — Segurança
O sistema deve garantir a proteção dos dados dos participantes em conformidade com a LGPD, utilizando criptografia para dados sensíveis e controle de acesso baseado em perfis (participante, organizador, equipe financeira, palestrante).

## RNF02 — Disponibilidade
O sistema deve ter disponibilidade mínima de 99,5%, com janelas de manutenção programadas em horários de baixo tráfego, especialmente fora dos períodos de inscrição de eventos.

## RNF03 — Desempenho
O sistema deve responder às requisições dos usuários em tempo inferior a 3 segundos para operações de consulta e inferior a 5 segundos para operações de inscrição e pagamento.

## RNF04 — Acessibilidade
O sistema deve seguir as diretrizes WCAG 2.1 nível AA, garantindo acessibilidade para pessoas com deficiência visual, motora e cognitiva.

## RNF05 — Privacidade de Dados
O sistema deve restringir o acesso aos dados dos participantes: palestrantes terão acesso apenas à lista nominal de inscritos em suas atividades, sem acesso a dados financeiros ou pessoais além do necessário.

## RNF06 — Escalabilidade
O sistema deve suportar picos de acesso durante períodos de abertura de inscrições, suportando no mínimo 500 usuários simultâneos sem degradação de performance.

## RNF07 — Auditabilidade
O sistema deve manter logs auditáveis de todas as operações críticas (inscrições, cancelamentos, pagamentos, reembolsos, emissão de certificados), com data, hora e usuário responsável.
