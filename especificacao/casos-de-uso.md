# Casos de Uso

## UC01 — Inscrever-se em Evento

**Ator Principal:** Participante
**Pré-condições:** O participante está autenticado. O evento possui vagas disponíveis.

### Fluxo Principal
1. O participante acessa a lista de eventos disponíveis.
2. O participante seleciona o evento desejado.
3. O sistema exibe as informações do evento (descrição, vagas, valor, política de cancelamento).
4. O participante confirma a inscrição.
5. O sistema verifica a disponibilidade de vagas.
6. O sistema registra a inscrição e decrementa o número de vagas.
7. O sistema envia o comprovante de inscrição ao participante.

### Fluxo Alternativo A — Evento Pago
6a. O sistema marca a inscrição como "aguardando pagamento" e reserva a vaga temporariamente.
6b. O participante é direcionado ao pagamento.
6c. Após confirmação do pagamento pela equipe financeira, a inscrição é confirmada.

### Fluxo Alternativo B — Evento Lotado
5a. O sistema identifica que não há vagas disponíveis.
5b. O sistema oferece ao participante a opção de entrar na lista de espera.
5c. O participante confirma interesse na lista de espera.

### Pós-condição
A inscrição é registrada (ou o participante é adicionado à lista de espera).

---

## UC02 — Cancelar Inscrição

**Ator Principal:** Participante
**Pré-condições:** O participante possui uma inscrição ativa. O evento permite cancelamento.

### Fluxo Principal
1. O participante acessa suas inscrições.
2. O participante seleciona a inscrição que deseja cancelar.
3. O sistema verifica se o evento permite cancelamento.
4. O sistema exibe a política de reembolso aplicável (se houver).
5. O participante confirma o cancelamento.
6. O sistema cancela a inscrição e libera a vaga.
7. O sistema notifica o participante do cancelamento.

### Fluxo Alternativo A — Lista de Espera Ativa
6a. O sistema identifica que há participantes na lista de espera.
6b. O sistema notifica o primeiro participante da lista sobre a vaga disponível.

### Fluxo de Exceção A — Evento Não Permite Cancelamento
3a. O sistema exibe mensagem informando que o evento não permite cancelamento.
3b. O caso de uso é encerrado.

### Pós-condição
A inscrição é cancelada e a vaga é liberada (ou o participante é informado que não pode cancelar).

---

## UC03 — Confirmar Pagamento

**Ator Principal:** Equipe Financeira
**Pré-condições:** Existe uma inscrição com status "aguardando pagamento".

### Fluxo Principal
1. A equipe financeira acessa a lista de inscrições aguardando pagamento.
2. A equipe financeira seleciona uma inscrição.
3. A equipe financeira verifica o comprovante de pagamento.
4. A equipe financeira confirma o pagamento no sistema.
5. O sistema altera o status da inscrição para "confirmada".
6. O sistema envia notificação de confirmação ao participante.

### Fluxo de Exceção A — Pagamento Não Confirmado
4a. A equipe financeira identifica que o pagamento não foi realizado.
4b. O sistema mantém o status "aguardando pagamento".
4c. Se o prazo expirar, o sistema libera a vaga.

### Pós-condição
A inscrição é confirmada ou a vaga é liberada.

---

## UC04 — Emitir Certificado

**Ator Principal:** Participante
**Pré-condições:** O participante possui inscrição confirmada. O evento foi concluído.

### Fluxo Principal
1. O participante acessa suas inscrições concluídas.
2. O participante seleciona o evento concluído.
3. O sistema verifica se o certificado está disponível para emissão.
4. O sistema gera o certificado em formato PDF.
5. O participante faz o download do certificado.

### Fluxo Alternativo A — Requer Confirmação de Presença
3a. O sistema identifica que o evento exige confirmação de presença.
3b. O sistema verifica se a presença foi confirmada pelo organizador.
3c. Se confirmada, o certificado é liberado. Caso contrário, exibe mensagem informativa.

### Pós-condição
O certificado é gerado e disponibilizado para download.

---

## UC05 — Cadastrar Evento

**Ator Principal:** Organizador
**Pré-condições:** O organizador está autenticado no sistema.

### Fluxo Principal
1. O organizador acessa a funcionalidade de cadastro de eventos.
2. O organizador preenche as informações do evento (nome, descrição, data, local, capacidade, tipo, política de cancelamento).
3. O organizador define se o evento é gratuito ou pago.
4. O organizador define a política de reembolso (se aplicável).
5. O organizador confirma o cadastro.
6. O sistema registra o evento e o disponibiliza para inscrição.

### Pós-condição
O evento é criado e disponível para inscrição dos participantes.
