# Processando um pagamento offline

## Necessidades
De posse da lista de possíveis de pagamentos, a pessoa pode selecionar uma forma e realizar o pedido. Alguns detalhes são importantes aqui. Todo pedido vem com as seguintes informações:
- O identificador para a forma de pagamento offline
- O identificador para o restaurante em questão
- O id do pedido em si (devemos consultar um sistema externo para saber o valor relacionado). Faça um get para um endpoint que simule o outro sistema. Você mesmo pode criar. O endereço deve ser acessado da seguinte forma: /api/pedidos/{idPedido} e é retornado um json representando um pedido. Neste caso só tem a informação do valor.
- O id do usuário em questão

Toda tentativa de transação para um pedido fica armazenada no sistema com as seguintes informações:
- id do pedido
- valor
- id do(a) usuário(a)
- status da transação
- Quando o pagamento for offline, a transação fica com status indicando que estamos esperando a confirmação do pagamento
- Exato instante de criação da transação
- Forma de pagamento escolhida.
- Informações extras sobre a forma de pagamento escolhida, caso seja necessário. No caso de pagamento offline, não precisa de nenhuma extra.

**Também é necessário que todas as transações fiquem registradas para posterior consulta no sistema.**

## Restrições
- o identificador para a forma de pagamento selecionada deve ser de um pagamento offline
- o identificador para o restaurante em questão é obrigatório
- o id do pedido deve existir no outro sistema
- a combinação de restaurante + usuário deve aceitar a forma de pagamento selecionada

## Resultado esperado
- Transação com forma de pagamento offline gerada com status de "esperando pagamento"
- Id da Transação retornada na resposta para que isso possa ser finalizada
- Caso exista alguma falha de validação, retorna o json adequado para a aplicação cliente.