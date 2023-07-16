# Processando um pagamento online(cartão)

## Necessidades
- o id do pedido em si (devemos consultar um sistema externo para saber o valor relacionado)
- faça um get para um endpoint que simule o outro sistema. Você mesmo pode criar. O endereço deve ser acessado da seguinte forma: /api/pedidos/{idPedido} e é retornado um json representando um pedido. Neste caso só tem a informação do valor.
- id do(a) usuário(a)
- status da transação
- Quando o pagamento for online, a transação fica com status indicando o resultado da operação. Sucesso ou falha
- Forma de pagamento escolhida que precisa ser online e cartão
- Precisamos do número do cartao e codigo de segurança.

### Fluxo para pagamentos online
Pagamentos online são processados por gateways.
Gateways possuem taxas sobre pagamento. Elas podem variar entre taxas fixas e percentuais em cima do valor da compra.
O nosso serviço precisa ser capaz de processar um pagamento online escolhendo um gateway de pagamento com custo mais baixo sempre.
Um outro detalhe importante é que no caso de falha por parte de algum gateway, precisamos tentar o próximo com custo mais baixo, até esgotar nossas possibilidades. Precisamos fazer de tudo para um pagamento ser processado!

### Sobre gateways e restrições
 - Gateway Seya opera no brasil, aceita todas bandeiras, tem custo fixo de 6.00.
 - Gateway Saori opera no brasil, só aceita visa e master, tem taxa percentual de 5% sobre a compra
 - Gateway Tango opera na argentina, aceita todas as bandeiras e tem custo que varia entre fixo e variável. Para compras de até 100 reais, o custo é fixo de 4.00. Para operações com valor maior que 100, o custo vira de 6% do valor total.


### Informação sobre integração com o gateway Seya
Para integrar com esse gateway são necessários dois passos.
 - Primeiro você precisa consultar uma api rest, através de post(usamos post por conta de possíveis requisitos de segurança como uso de https), verificando se o número do cartão e o código de segurança são realmente aceitos. Você pode passar os dados via json.
 - para o número do cartão use o parâmetro num_cartao
 - para o código de segurança use o parâmetro codigo_seguranca
 - Em caso de sucesso, é retornado um status de sucesso e um id diretamente no corpo da resposta referente a aquele processamento.
 - O próximo passo é usar o id retornado para compor o endereço de acesso, passar mais uma vez as infos de cartao e agora também o valor da compra. Caso o id gerado não exista, é retornado 404.
 - para o valor o parâmetro chama valor_compra


### Informação sobre integração com o gateway Saori
Para esse gateway é necessário apenas um passo, passando as informações do cartão + valor.
- Você precisa acessar uma api rest, através de post, passando número do cartão, codigo de segurança e valor. Os dados podem ir via json.
- para o número do cartão use o parâmetro num_cartao
- para o código de segurança use o parâmetro codigo_seguranca
- para o valor o parâmetro chama valor_compra

### Informação sobre integração com o gateway Tango
Aqui você precisa passar um json para um endpoint usando o post com o valor e dados do cartão.
- para o número do cartão use a chave "numero_cartao"
- para o código de segurança use a chave "codigo_seguranca"
- para o valor use a chave "valor_compra"

**Novos gateways podem ser adicionados e o sistema precisa estar preparado**


### O que precisa acontecer depois do processamento
- Toda tentativa de transação para um pedido fica armazenada no sistema com as seguintes informações:
- id do pedido
- valor
- id do(a) usuário(a)
- status da transação
- Quando o pagamento for offline, a transação fica com status indicando que estamos esperando a confirmação do pagamento
- Quando o pagamento for online, no fluxo normal deve ter uma transação marcando o começo e uma marcando a conclusão.
- Exato instante de criação da transação
- Forma de pagamento escolhida.
- Informações extras sobre a forma de pagamento escolhida, caso seja necessário. No caso de pagamento offline, não precisa de nenhuma extra.
- Também é necessário que todas as transações fiquem registradas para posterior consulta no sistema.

## Restrições
- o identificador para a forma de pagamento selecionada deve ser de um pagamento online
- o identificador para o restaurante em questão é obrigatório
- o id do pedido deve existir no outro sistema
- a combinação de restaurante + usuário deve aceitar a forma de pagamento selecionada
- Um pagamento só não é processado se todos as integrações falhare

## Resultado esperado
- Pagamento online processado(ou tentado até a morte), transação registrada com todas as informações já faladas status de concluída.
- Caso um pagamento não possa ser processado, deve ser retornado o status 402(https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status/402). Este é um status ainda com seu uso em aberto, mas ele foi reservado para ecommerces. Vamos usá-lo :