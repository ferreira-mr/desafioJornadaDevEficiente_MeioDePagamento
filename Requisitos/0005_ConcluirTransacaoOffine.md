# Conclusão de uma transação offline

## Necessidades
- Precisamos receber o codigo do pedido que marcou o começo do processo e gerar uma nova transacao para tal pedido com o status de concluída.

## Restrições
- precisa existir uma transacao iniciada para aquele pedido
- dado um pedido, só pode ter uma transacao concluida.

## Resultado esperado
- status indicando que a transação foi concluída com sucesso
- Caso aconteça algum problema de validação, retorne 400 para indicar.