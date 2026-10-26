# Análise dos Ajustes de Prompts

## Como cada tipo de prompt influenciou a qualidade e a diversidade

- **Zero-shot com contrato OpenAPI:** produziu casos tecnicamente aderentes ao contrato (fluxo feliz, falha de pagamento, evento lotado), mas tendeu a gerar apenas fluxos "esperados", com pouca exploração de falhas de infraestrutura (timeout, indisponibilidade, concorrência).
- **Few-shot com exemplos:** foi o que mais melhorou a consistência de formato — todos os casos saíram no mesmo padrão — e ampliou a diversidade ao incluir explicitamente casos de erro (timeout, contrato inválido), pois os exemplos "ensinaram" o nível de detalhe esperado.
- **Chain-of-thought:** foi o mais valioso para profundidade — ao forçar a análise de dependências e pontos de falha, revelou cenários que não apareceram nos prompts anteriores, como concorrência na última vaga, idempotência de pagamento e falha no serviço de notificações com reprocessamento via fila (DLQ).

## Ajustes de prompt necessários

- **Primeira versão do zero-shot:** gerou cenários genéricos, sem dados concretos e sem códigos HTTP. **Ajuste aplicado:** incluir a especificação OpenAPI e as regras de negócio no prompt — os casos ficaram aderentes ao contrato.
- **Primeira versão do few-shot:** sem exemplos, o formato saía inconsistente. **Ajuste aplicado:** incluir 2 exemplos completos — consistência total e maior cobertura de erros.
- **Chain-of-thought:** o raciocínio explícito gerava texto extenso. **Ajuste aplicado:** delimitar a saída final a casos estruturados, mantendo a análise como etapa interna — melhor equilíbrio entre profundidade e usabilidade.
- **Aprendizado geral:** pedir explicitamente "casos de erro" e "cenários de falha" é essencial — sem isso, a LLM tende a gerar apenas fluxos felizes. A GenAI atua como um excelente copiloto, mas o julgamento humano continua sendo necessário para validar relevância, viabilidade e cobertura dos cenários.
