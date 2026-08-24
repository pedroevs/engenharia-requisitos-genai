# Requisitos Funcionais

## RF01 — Cadastrar Evento
O sistema deve permitir que o organizador cadastre novos eventos, informando nome, descrição, data, local, capacidade máxima de vagas, tipo (gratuito ou pago) e política de cancelamento.

## RF02 — Consultar Eventos Disponíveis
O sistema deve permitir que o participante visualize todos os eventos disponíveis para inscrição, com informações de vagas restantes e status (aberto, lotado, encerrado).

## RF03 — Inscrever-se em Evento
O sistema deve permitir que o participante se inscreva em eventos e workshops, recebendo um comprovante de inscrição ao concluir o processo.

## RF04 — Cancelar Inscrição
O sistema deve permitir que o participante cancele sua inscrição, desde que o evento permita cancelamento, conforme política definida pelo organizador.

## RF05 — Emitir Certificado
O sistema deve permitir que o participante emita seu certificado de participação após a conclusão do evento, seja automaticamente ou mediante confirmação de presença.

## RF06 — Controlar Vagas Automaticamente
O sistema deve controlar automaticamente o número de vagas disponíveis para cada evento, decrementando o total ao receber uma nova inscrição e incrementando ao receber um cancelamento.

## RF07 — Gerenciar Lista de Espera
O sistema deve criar automaticamente uma lista de espera quando um evento atingir o limite de vagas, permitindo que participantes interessados sejam notificados quando vagas forem liberadas.

## RF08 — Confirmar Pagamento
O sistema deve permitir que a equipe financeira confirme o pagamento de inscrições em eventos pagos, liberando a vaga do participante somente após a confirmação.

## RF09 — Processar Reembolso
O sistema deve permitir que a equipe financeira processe reembolsos de inscrições canceladas, respeitando as regras de reembolso definidas para cada evento.

## RF10 — Consultar Inscritos em Atividades
O sistema deve permitir que o palestrante consulte a lista de participantes inscritos em suas atividades, respeitando as políticas de privacidade de dados.

## RF11 — Acompanhar Inscrições em Tempo Real
O sistema deve permitir que o organizador acompanhe a quantidade de inscritos em tempo real, com indicadores de vagas preenchidas, disponíveis e lista de espera.

## RF12 — Enviar Comprovante e Notificações
O sistema deve enviar automaticamente comprovantes de inscrição e notificações aos participantes (confirmação de pagamento, cancelamento, liberação de vaga na lista de espera, emissão de certificado).

## RF13 — Gerenciar Participantes
O sistema deve permitir que o organizador gerencie os participantes inscritos, incluindo visualização, edição de informações e remoção de registros.

## RF14 — Inscrição em Workshops Simultâneos
O sistema deve permitir que o participante se inscreva em workshops que acontecem no mesmo dia, desde que não haja conflito de horário entre as atividades.
