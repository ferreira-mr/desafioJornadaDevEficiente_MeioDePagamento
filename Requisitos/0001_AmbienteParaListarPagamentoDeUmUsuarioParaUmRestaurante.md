# Criação do ambiente necessário para listar pagamentos de um determinado usuário para um determinado restaurante

## Necessidades
Precisamos criar o código necessário para conseguir listar as formas de pagamento disponíveis para um determinado usuário.

### Um usuário tem as seguintes informações:
 - email(obrigatório e com formatação de email)
 - um conjunto de formas de pagamento que ele(a) pode usar (pelo menos uma)
 - Uma forma de pagamento tem as seguintes informações (não muda muito)
 - tipo(cartão, dinheiro, maquina,cheque) (obrigatório)
 - Cartão pode ser usado para pagamento online
 - Os outros tipos pagam offline
 - Descrição(poucas palavras explicar a forma) - (obrigatório)
É importante lembrar que você pode ter muitas bandeiras de cartões diferentes(master,visa,elo,hypercard).


### Um restaurante tem as seguintes informações
- Nome (obrigatório)
- Um conjunto de formas de pagamento que ele aceita (pelo menos uma)

Reforçando, modele e faça o necessário para termos essa representação no código e também com dados gravados no banco de dados.

Não existe um jeito certo de modelar, dado que sirva para os propósitos do software e que possa entendido por outras pessoas, deve estar certo :).

## Restrições

## Resultado esperado
- odelagem inicial feita
- Massa de dados gerada para que possamos trabalhar em cima.