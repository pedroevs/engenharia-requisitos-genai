# Critérios de Aceitação

## US01 — Consultar eventos disponíveis
- O sistema deve exibir todos os eventos com inscrições abertas.
- Cada evento deve mostrar: nome, data, local, vagas disponíveis e status.
- Eventos lotados devem ser exibidos com a opção "Entrar na lista de espera".
- Eventos encerrados não devem aparecer na lista de eventos disponíveis.

## US02 — Inscrever-se em evento
- O participante deve conseguir concluir a inscrição em no máximo 5 cliques.
- O comprovante de inscrição deve ser enviado automaticamente após a confirmação.
- Em eventos pagos, a inscrição deve ficar com status "aguardando pagamento" até a confirmação.
- O número de vagas deve ser decrementado imediatamente após a confirmação (ou reserva temporária).

## US03 — Inscrever-se em workshops simultâneos
- O sistema deve permitir a inscrição em workshops no mesmo dia com horários diferentes.
- O sistema deve impedir a inscrição em workshops com horários sobrepostos.
- O sistema deve exibir um alerta quando o participante tentar se inscrever em atividades conflitantes.

## US04 — Cancelar inscrição
- O sistema deve permitir o cancelamento apenas de eventos que permitem essa opção.
- A política de cancelamento deve ser exibida antes da confirmação.
- Ao cancelar, a vaga deve ser liberada imediatamente.
- Se houver lista de espera, o primeiro participante deve ser notificado automaticamente.
- O participante deve receber confirmação do cancelamento.

## US05 — Emitir certificado
- O certificado só deve estar disponível após a conclusão do evento.
- Se o evento exigir confirmação de presença, o certificado só deve ser emitido após a confirmação.
- O certificado deve ser gerado em formato PDF com nome do participante, nome do evento e carga horária.
- O participante deve conseguir baixar o certificado quantas vezes quiser.

## US06 — Cadastrar evento
- Todos os campos obrigatórios devem ser validados (nome, data, local, capacidade).
- A capacidade máxima deve ser um número inteiro positivo.
- O sistema deve exigir a definição da política de cancelamento no cadastro.
- O evento deve aparecer imediatamente na lista de eventos disponíveis após o cadastro.

## US07 — Controlar vagas automaticamente
- O contador de vagas deve atualizar em tempo real a cada nova inscrição.
- Ao atingir zero vagas, o evento deve mudar automaticamente para o status "lotado".
- Cancelamentos devem incrementar o contador de vagas imediatamente.

## US08 — Criar lista de espera
- A lista de espera deve ser ativada automaticamente quando o evento lotar.
- O participante deve receber uma posição na lista de espera.
- Ao liberar uma vaga, o primeiro da lista deve ser notificado.
- O participante notificado deve ter um prazo definido para confirmar a inscrição.

## US09 — Acompanhar inscrições em tempo real
- O painel deve mostrar: total de vagas, vagas preenchidas, vagas disponíveis e tamanho da lista de espera.
- Os números devem atualizar em tempo real sem necessidade de refresh.

## US10 — Confirmar pagamentos e processar reembolsos
- A equipe financeira deve visualizar todas as inscrições com status "aguardando pagamento".
- Ao confirmar o pagamento, a inscrição deve mudar para "confirmada" e o participante deve ser notificado.
- O reembolso deve seguir a política definida no cadastro do evento.
- O sistema deve registrar o log de todas as operações financeiras.

## US11 — Consultar inscritos em minhas atividades
- O palestrante deve visualizar apenas os participantes inscritos em suas atividades.
- Dados financeiros dos participantes não devem ser exibidos.
- A lista deve mostrar: nome do participante e atividade inscrita.
- O acesso deve ser restrito às atividades vinculadas ao palestrante autenticado.
