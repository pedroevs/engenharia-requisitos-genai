# Prompt 2 — Few-shot com exemplos (foco: casos de erro e consistência de formato)
 
Você é um engenheiro de QA. Gere casos de teste de integração para o fluxo entre o Serviço de Inscrições e o Serviço de Pagamentos, seguindo EXATAMENTE o formato dos exemplos abaixo:
 
Exemplo 1:
ID: CTI-001
Descrição: Inscrição confirmada após pagamento aprovado
Pré-condições: evento com vagas; participante cadastrado
Passos: 1. POST /inscricoes {idEvento: 101, idParticipante: 5001, tipoIngresso: "padrao"} 2. POST /pagamentos {idInscricao: <retornado>, valor: 100.00, metodoPagamento: "cartao"}
Dados: cartão com saldo
Resultado esperado: HTTP 201 na inscrição; HTTP 200 no pagamento; status = CONFIRMADA; vagas decrementadas
 
Exemplo 2:
ID: CTI-002
Descrição: Inscrição cancelada quando pagamento é recusado
Pré-condições: evento com vagas; participante cadastrado
Passos: 1. POST /inscricoes {idEvento: 101, idParticipante: 5001, tipoIngresso: "padrao"} 2. POST /pagamentos {idInscricao: <retornado>, valor: 100.00, metodoPagamento: "cartao"} com cartão recusado (código 51)
Dados: cartão recusado (código 51)
Resultado esperado: HTTP 402 no pagamento; inscrição CANCELADA; vaga NÃO decrementada
 
Agora gere 4 casos adicionais cobrindo: timeout no pagamento, evento lotado, cancelamento com notificação à lista de espera e resposta de contrato inválido. Mantenha o mesmo formato.
