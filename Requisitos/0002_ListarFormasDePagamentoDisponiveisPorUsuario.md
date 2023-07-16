# Listagem de formas de pagamentos disponíveis para um usuário

## Necessidades
Dado o id de um restaurante e o id do usuario, precisamos retornar as formas de pagamento que o usuário em questão aceita e que também são permitidas pelo restaurante.

O retorno esperado é o seguinte:
- Descricao da forma de pagamento
- Id da forma de pagamento

## Restrições
- Id do restaurante é obrigatório
- Id do usuário é obrigatório

## Resultado esperado
- Status 200 com um json informando a descrição e o id da forma de pagamento escolhida
