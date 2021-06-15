# Bem vindo!

Obrigado pelo interesse em integrar a sua aplicação a nossa plataforma!
Isto facilitará o dia a dia das operações nos restaurtates parceiros, que por muitas vezes, tem um fluxo muito grande de pedidos e é necessário uma automação, para uma melhor operação interna e evitar possíveis erros humanos.

Criamos uma API de fácil integração no qual não haverá dificuldades no desenvolvimento, mas caso apareça algum, lembre-se: Estamos aqui para te ajudar no que for preciso!

Então!? Vamos comerçar?

----

# Primeiros passos

Após realizar o cadastro do estabelecimento na área do parceiro, será gerado um [TOKEN](https://medium.com/tableless/entendendo-tokens-jwt-json-web-token-413c6d1397f6) de acesso a ser enviado em cada requisição no **header** no parâmetro **posToken**.

Exemplo:

    posToken: "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJmMTNkNjk3MC00ODIwLTRhYmQtOGNiZS1jNjA1ZDkwZDEwN2IiLCJqdGkiOiI2MjYwZjE0Zi04MTJjLTQwMjctYWQ5OC01ZmI3MGJkMjA5OTcifQ.fUJG6Sfb3bb0m74R_Yeujz4exXQhdQfeLbsKWbbfabC"

## Atenção!
A URL desta documentação está apontada para nossa base de testes/homologação:

    https://api.onpub.com.br/dev/

A URL de produção é:

    https://api.onpub.com.br/v1/

## Código de integração

No [portal do estabelecimento](https://portal.onpub.com.br) clique no perfil do restaurante marque a opção: **Integração com PDV**

<img src="https://firebasestorage.googleapis.com/v0/b/onpub-production.appspot.com/o/docs%2FPosOption.png?alt=media&token=82ab7cec-3c41-4efa-8a3c-95e845b78912" alt="OnPub Pub Integration PDV" style="float: left; margin-right: 10px;" />

>Marcado esta opção, apenas os produtos com código de integração estarão disponíveis no cardápio do aplicativo.

Para o integrar produtos, complementos e garçons, é necessário informar o código de integração em seu cadastro, dentro [portal do estabelecimento](https://portal.onpub.com.br)

<img src="https://firebasestorage.googleapis.com/v0/b/onpub-production.appspot.com/o/docs%2FIntegrationIdProduct.png?alt=media&token=9fb8b844-2119-4b7b-934d-9708d699b4df" alt="OnPub Product Integration Id" style="float: left; margin-right: 10px;" />


>**Atenção!** Caso o estabelecimento seja configurado para ter uma integração com o PDV, os produtos  que não tiverem o código de integração não estarão disponíveis no cardápio do aplicativo.

## Exemplo com fontes
|Linguagem|Link para download|
|---|---|
|Delphi|https://drive.google.com/open?id=11p_wHvWWKxR23IiJpESqPcegXa8ADUah|

## Checklist de homologação

Para testar todas as funções do Onpub e do PDV relativo a integração, criamos um checklist de homologação para que seja realizado antes da liberação do ambiente de produção.
[Clique aqui](https://drive.google.com/open?id=14XEBvpqMwX70S39dz-TQScCYdx82AxhB) para baixar.

## Histórico de atualizações
|Data|Versão|Histórico|
|---|---|---|
|02/04/2019|1.0.001|Lançamento da documentação|
|10/04/2019|1.0.002|Adição do evento **USER_CHANGE** e método *usersLogged*|
|30/04/2019|1.0.003|Incluído link exemplo em Delphi|
|15/05/2019|1.0.004|Visualização dos produtos no cardápio do aplicativo apenas os que tem o código de integração informado|
|22/05/2019|1.0.005|Adição dos endpoints do cardápio|
|29/05/2019|1.0.006|Adição da forma de pagamento PicPay|
|30/05/2019|1.0.007|Adição do checklist de homologação. Inclusão da função de limpar o cardápio|
|03/06/2918|1.0.008|Adição do campo *priceCalculation* no item do complemento|

----

# HTTP Satus Code

Para auxilio na utilização da API, segue a legenda dos status HTTP que podem ser recebidas pelo Client. Para ter uma base de cada evento recebido pela API, você pode se basear nos seguintes códigos.

## 400 - Bad Request
Geralmente ocorre quando o cliente envia uma requisição contendo um JSON inválido no body, order ou reference inválido ou ausência de campos obrigatórios. (exemplo: event sem o id).

>Solução:
Verifique o body da requisição, campos obrigatórios e a estrutura da requisição. Caso tenha alguma duvida sobre a composição, pode olhar nos exemplos disponíveis nos próprios endpoints.

## 401 - Unauthorized
O Unauthorized ocorre por estar tentando realizar uma ação que o e-PDV não tem permissão, no geral, a chamada está correta e faltam as credenciais corretas. O mais comum é que as requisições para as APIs estejam sem o token de acesso ou o token está expirou.

>Solução:
Obtenha um novo token via /oauth/token antes da utilização das APIs. Caso ainda persista, verifique se o seu token possui permissão para acessar a loja informada.

## 403 - Forbidden
Ocorre quando o e-PDV não possui permissão de realizar a operação e nova requisição não resultará em sucesso. Exemplo: e-PDV tenta recuperar detalhes de um pedido que não pertence a nenhum restaurante sob seu controle

>Solução:
Verifique o body da requisição e seus parâmetros. Caso todos os parametros estejam corretos, entre em contato conosco via suporte.

## 404 - Not found
Não é necessariamente um erro. O servidor pode responder com status 404 quando todos eventos já foram consumidos pelo e-PDV (events:polling). Outra situação onde 404 pode ocorrer é quando o servidor recebe um requisição sobre detalhes de um pedido não existente.

>Solução:
No caso da referência do pedido ser inválida, reenvie a requisição com a referência correta.

## 500 - Internal server error
Mensagem de erro genérica quando uma condição inesperada foi encontrada.

>Solução:
Contate os administradores do sistema IFood através da página de suporte.

## 503 - Service unavailable
Indica que a API OnPub está tendo problemas para responder as requisições dentro do tempo esperado ou está fora de serviço para manutenção.

>Solução:
Provavelmente deve-se tratar de uma indisponibilidade temporária e você pode tentar reenviar a requisição. Caso o problema ocorra por mais de 30 minutos, você pode nos contatar através da página de suporte.

## 200 - Ok
Indica que a requisição foi processada com sucesso, geralmente retornada no events:polling.

## 201 - Created
Indica que os novos parâmetros foram recebido com sucesso.

## 202 - Accepted
Indica que o endpoint foi recebido e suas informações foram inseridas com sucesso.

----