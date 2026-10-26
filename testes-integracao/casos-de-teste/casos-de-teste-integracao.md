# Casos de Teste de Integração Gerados com IA Generativa

## Tabela-resumo

| ID | Descrição | Resultado esperado (resumo) |
|---|---|---|
| CTI-001 | Inscrição confirmada após pagamento aprovado (fluxo feliz) | 201 inscrição; 200 pagamento; status CONFIRMADA; vaga decrementada |
| CTI-002 | Inscrição cancelada quando pagamento é recusado | 402 pagamento; inscrição CANCELADA; vaga NÃO decrementada |
| CTI-003 | Timeout no serviço de pagamentos | Retry com backoff; consistência eventual; inscrição PENDENTE |
| CTI-004 | Evento lotado no momento da inscrição | 409; lista de espera criada; participante notificado |
| CTI-005 | Cancelamento libera vaga e notifica primeiro da lista de espera | Vaga incrementada; notificação ao primeiro da fila |
| CTI-006 | Concorrência: duas inscrições simultâneas na última vaga | Apenas uma confirmada; outra vai para lista de espera |
| CTI-007 | Resposta de contrato inválido do serviço de pagamentos | Erro de desserialização tratado; inscrição PENDENTE; alerta |
| CTI-008 | Falha no serviço de notificações | Inscrição mantida; notificação enfileirada (DLQ) |
| CTI-009 | Idempotência: requisição de pagamento duplicada | Segunda chamada retorna mesmo resultado; pago uma única vez |
| CTI-010 | Inscrição em evento inexistente | 404 propagado; nenhum efeito colateral |

## Detalhamento completo dos casos

### CTI-001 — Inscrição confirmada após pagamento aprovado (fluxo feliz)

- **Descrição:** Validar o fluxo completo de inscrição com pagamento aprovado, confirmando a integração entre os serviços de Inscrições e Pagamentos.
- **Pré-condições:** Evento com vagas disponíveis; participante cadastrado; serviços de Inscrições e Pagamentos operacionais.
- **Passos:**
  1. POST /inscricoes com body {idEvento: 101, idParticipante: 5001, tipoIngresso: "padrao"} — esperar HTTP 201 e capturar o idInscricao retornado.
  2. POST /pagamentos com body {idInscricao: <id retornado>, valor: 100.00, metodoPagamento: "cartao"} — esperar HTTP 200.
  3. GET /inscricoes/{id} — verificar o status da inscrição.
- **Dados de teste:** Cartão com saldo suficiente; evento 101 com capacidade 100 e 90 inscritos.
- **Resultado esperado:** HTTP 201 na inscrição; HTTP 200 no pagamento; status da inscrição = CONFIRMADA; vagas decrementadas de 10 para 9.

### CTI-002 — Inscrição cancelada quando pagamento é recusado

- **Descrição:** Validar que uma inscrição é cancelada quando o pagamento é recusado, garantindo que a vaga não seja consumida.
- **Pré-condições:** Evento com vagas; participante cadastrado; serviço de Pagamentos configurado para recusar cartão com código 51.
- **Passos:**
  1. POST /inscricoes com body {idEvento: 101, idParticipante: 5002, tipoIngresso: "padrao"} — esperar HTTP 201.
  2. POST /pagamentos com body {idInscricao: <id retornado>, valor: 100.00, metodoPagamento: "cartao"} — cartão recusado (código 51) — esperar HTTP 402.
  3. GET /inscricoes/{id} — verificar o status da inscrição.
- **Dados de teste:** Cartão recusado com código 51 (fundos insuficientes).
- **Resultado esperado:** HTTP 402 no pagamento; inscrição com status CANCELADA; vaga NÃO decrementada (permanece 10).

### CTI-003 — Timeout no serviço de pagamentos

- **Descrição:** Validar o comportamento do sistema quando o serviço de Pagamentos excede o tempo limite de resposta.
- **Pré-condições:** Serviço de Pagamentos com latência simulada superior ao timeout configurado (ex.: > 5 segundos); inscrição criada.
- **Passos:**
  1. POST /inscricoes — esperar HTTP 201.
  2. POST /pagamentos — o serviço não responde dentro do timeout.
  3. Verificar a política de retry aplicada (número de tentativas e backoff).
  4. GET /inscricoes/{id} — verificar o status após o processamento.
- **Dados de teste:** Latência simulada de 10 segundos no serviço de Pagamentos; timeout configurado em 5 segundos.
- **Resultado esperado:** Retry com política de backoff (ex.: 3 tentativas com backoff exponencial); consistência eventual; inscrição permanece PENDENTE até a confirmação do pagamento; nenhuma vaga decrementada antes da confirmação.

### CTI-004 — Evento lotado no momento da inscrição

- **Descrição:** Validar que, quando a capacidade máxima do evento é atingida, o sistema cria automaticamente uma lista de espera.
- **Pré-condições:** Evento com capacidade máxima atingida (100/100 inscritos).
- **Passos:**
  1. POST /inscricoes com body {idEvento: 101, idParticipante: 5003, tipoIngresso: "padrao"} — esperar HTTP 409.
  2. Verificar se o participante foi adicionado à lista de espera.
  3. Verificar se o participante foi notificado sobre a entrada na lista de espera.
- **Dados de teste:** Evento 101 com capacidade 100 e 100 inscritos confirmados.
- **Resultado esperado:** HTTP 409 (Conflito); lista de espera criada automaticamente com o participante 5003; notificação enviada ao participante informando a posição na fila.

### CTI-005 — Cancelamento libera vaga e notifica primeiro da lista de espera

- **Descrição:** Validar que o cancelamento de uma inscrição confirmada libera a vaga e notifica o primeiro participante da lista de espera.
- **Pré-condições:** Evento lotado com lista de espera contendo pelo menos 1 participante; existe uma inscrição confirmada para cancelar.
- **Passos:**
  1. DELETE /inscricoes/{id} da inscrição confirmada — esperar HTTP 204.
  2. Verificar se a vaga foi incrementada.
  3. Verificar se o primeiro da lista de espera foi notificado com prazo para confirmação.
- **Dados de teste:** Lista de espera com participante 5003 na primeira posição; inscrição confirmada do participante 5001.
- **Resultado esperado:** HTTP 204 no cancelamento; vaga incrementada de 0 para 1; notificação enviada ao primeiro da lista de espera (participante 5003) com prazo para confirmar a vaga (ex.: 24 horas).

### CTI-006 — Concorrência: duas inscrições simultâneas na última vaga

- **Descrição:** Validar o controle de concorrência quando duas requisições de inscrição chegam simultaneamente para a última vaga disponível.
- **Pré-condições:** Evento com exatamente 1 vaga restante (99/100 inscritos).
- **Passos:**
  1. Disparar POST /inscricoes (requisição A, participante 5004) e POST /inscricoes (requisição B, participante 5005) simultaneamente.
  2. Verificar o resultado de cada requisição.
  3. Verificar o status final das duas inscrições.
- **Dados de teste:** Evento 101 com 99 inscritos confirmados; duas requisições concorrentes.
- **Resultado esperado:** Apenas uma das requisições é confirmada (HTTP 201); a outra recebe HTTP 409 e vai para a lista de espera; o controle de concorrência (locking otimista ou transação atômica) impede a venda duplicada da última vaga.

### CTI-007 — Resposta de contrato inválido do serviço de pagamentos

- **Descrição:** Validar o tratamento de erro quando o serviço de Pagamentos retorna um payload fora do contrato esperado.
- **Pré-condições:** Serviço de Pagamentos configurado para retornar payload malformado (ex.: campo status ausente ou tipo incorreto).
- **Passos:**
  1. POST /inscricoes — esperar HTTP 201.
  2. POST /pagamentos — o serviço retorna resposta com contrato inválido.
  3. Verificar o tratamento do erro de desserialização.
  4. GET /inscricoes/{id} — verificar o status.
- **Dados de teste:** Resposta do pagamento sem o campo "status" ou com tipo inesperado.
- **Resultado esperado:** Erro de desserialização tratado adequadamente (sem crash do orquestrador); inscrição permanece PENDENTE; alerta de monitoramento gerado para investigação.

### CTI-008 — Falha no serviço de notificações

- **Descrição:** Validar que a falha no serviço de Notificações não compromete a inscrição e que a notificação é reprocessada.
- **Pré-condições:** Serviço de Notificações indisponível (simulado); fluxo de inscrição e pagamento operacional.
- **Passos:**
  1. Executar o fluxo feliz: POST /inscricoes + POST /pagamentos — ambos com sucesso.
  2. Verificar a tentativa de envio da notificação de confirmação.
  3. Verificar se a notificação foi enfileirada para reprocessamento.
- **Dados de teste:** Serviço de Notificações retornando HTTP 503.
- **Resultado esperado:** Inscrição mantida como CONFIRMADA (a falha de notificação não reverte a inscrição); notificação enfileirada em DLQ (dead letter queue) para reprocessamento posterior; alerta de monitoramento gerado.

### CTI-009 — Idempotência: requisição de pagamento duplicada

- **Descrição:** Validar que o serviço de Pagamentos processa uma requisição duplicada apenas uma única vez.
- **Pré-condições:** Inscrição criada; serviço de Pagamentos com suporte a idempotency key.
- **Passos:**
  1. POST /pagamentos com idempotency key "KEY-001" — esperar HTTP 200.
  2. POST /pagamentos com a MESMA idempotency key "KEY-001" e mesmo body — verificar o resultado.
  3. Verificar se o pagamento foi processado apenas uma vez (consultar extrato/transações).
- **Dados de teste:** Mesma idempotency key e mesmo payload nas duas chamadas.
- **Resultado esperado:** A segunda chamada retorna o mesmo resultado da primeira (HTTP 200 com mesmo status); o pagamento é processado uma única vez; nenhuma cobrança duplicada.

### CTI-010 — Inscrição em evento inexistente

- **Descrição:** Validar o comportamento do sistema quando a inscrição referencia um evento que não existe.
- **Pré-condições:** idEvento inexistente no banco de dados.
- **Passos:**
  1. POST /inscricoes com body {idEvento: 99999, idParticipante: 5006, tipoIngresso: "padrao"} — esperar HTTP 404.
  2. Verificar que nenhum efeito colateral foi gerado (nenhuma chamada ao serviço de Pagamentos).
- **Dados de teste:** idEvento 99999 (inexistente).
- **Resultado esperado:** HTTP 404 propagado corretamente pelo serviço de Inscrições; nenhuma chamada ao serviço de Pagamentos; nenhuma vaga alterada.
