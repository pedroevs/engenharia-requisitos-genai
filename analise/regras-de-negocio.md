# Regras de Negócio

## RN01 — Controle Automático de Vagas
O sistema deve decrementar o número de vagas disponíveis automaticamente ao confirmar uma inscrição e incrementar ao processar um cancelamento válido.

## RN02 — Política de Cancelamento por Evento
Cada evento define sua própria política de cancelamento. Alguns eventos permitem cancelamento até uma data limite, outros não permitem. Esta informação deve ser exibida ao participante antes da inscrição.

## RN03 — Lista de Espera Automática
Quando um evento atinge o limite de vagas, o sistema abre automaticamente uma lista de espera. Quando uma vaga é liberada por cancelamento, o primeiro participante da lista deve ser notificado e ter um prazo para confirmar a inscrição.

## RN04 — Eventos Gratuitos e Pagos
O sistema deve diferenciar eventos gratuitos (inscrição confirmada imediatamente) de eventos pagos (inscrição confirmada apenas após validação do pagamento pela equipe financeira).

## RN05 — Reembolso Condicional
O reembolso de inscrições canceladas segue regras definidas por evento: alguns oferecem reembolso integral até uma data limite, outros reembolso parcial, e outros não oferecem reembolso.

## RN06 — Confirmação de Pagamento Obrigatória
Em eventos pagos, a vaga é reservada temporariamente no momento da inscrição, mas só é confirmada após a equipe financeira validar o pagamento. Se o pagamento não for confirmado dentro do prazo, a vaga é liberada.

## RN07 — Inscrição em Workshops Simultâneos
O participante pode se inscrever em workshops no mesmo dia, desde que não haja sobreposição de horários. O sistema deve impedir a inscrição em atividades com horários conflitantes.

## RN08 — Acesso Restrito de Palestrantes
Palestrantes têm acesso apenas à lista de participantes inscritos em suas próprias atividades. Dados financeiros e dados pessoais além do nome não devem ser exibidos.

## RN09 — Emissão de Certificado
O certificado deve ser emitido após a conclusão do evento. A emissão pode ser automática ou depender da confirmação de presença pelo organizador.
