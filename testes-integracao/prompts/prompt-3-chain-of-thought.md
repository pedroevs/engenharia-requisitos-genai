# Prompt 3 — Chain-of-thought (foco: análise de dependências e pontos de falha)
 
Você é um engenheiro de QA. Antes de gerar os casos de teste de integração, realize explicitamente as seguintes etapas:
 
Etapa 1: liste as dependências entre os serviços (Inscrições, Pagamentos, Notificações);
Etapa 2: identifique os pontos de falha possíveis em cada chamada (timeout, erro de contrato, indisponibilidade, dados inconsistentes);
Etapa 3: descreva o comportamento esperado em cada ponto de falha (retry, rollback, compensação, fila);
Etapa 4: somente depois, gere os casos de teste de integração no formato: ID, descrição, pré-condições, passos, dados e resultado esperado.
