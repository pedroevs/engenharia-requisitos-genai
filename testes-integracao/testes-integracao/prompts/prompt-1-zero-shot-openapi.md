# Prompt 1 — Zero-shot com contrato OpenAPI (foco: cenários válidos)
 
Você é um engenheiro de QA especializado em testes de integração de APIs REST. Abaixo está a especificação OpenAPI simplificada de dois serviços de um Sistema de Gestão de Eventos:
 
[SERVIÇO DE INSCRIÇÕES]
- POST /inscricoes — cria inscrição (body: idEvento, idParticipante, tipoIngresso)
- DELETE /inscricoes/{id} — cancela inscrição
- GET /inscricoes/{id} — consulta inscrição
 
[SERVIÇO DE PAGAMENTOS]
- POST /pagamentos — processa pagamento (body: idInscricao, valor, metodoPagamento)
- GET /pagamentos/{id} — consulta status do pagamento
 
Regras de negócio: a inscrição só é confirmada após pagamento aprovado; vagas são decrementadas na confirmação e incrementadas no cancelamento; evento lotado cria lista de espera.
 
Gere 6 casos de teste de integração cobrindo: fluxo feliz, falha de pagamento, timeout, evento lotado, cancelamento e concorrência. Para cada caso, informe: ID, descrição, pré-condições, passos (chamadas HTTP), dados de teste e resultado esperado.
