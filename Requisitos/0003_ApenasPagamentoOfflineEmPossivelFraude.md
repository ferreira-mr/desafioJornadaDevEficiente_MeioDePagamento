# Caso a pessoa seja considerada uma possível fraudadora, só deve estar disponível as formas de pagamento offline.

## Necessidades
O nosso serviço tem uma regra que verifica se a pessoa é uma possível fraudadora de pagamentos online. Para não complicarmos o algoritmo da regra em si, simplesmente defina um conjunto de emails que são considerados de possíveis fraudadores(as).

Neste regra em específico se a pessoa for considerada uma fraudadora, a regra só aceita formas de pagamento offline.

Nosso serviço deve ser capaz de acrescentar novas regras de fraude que sejam capaz de filtrar a combinação entre usuário e forma de pagamento sem muita dificuldade.

## Resultado esperado
Lista de pagamentos respeitando as regras de possíveis fraudadores(as).