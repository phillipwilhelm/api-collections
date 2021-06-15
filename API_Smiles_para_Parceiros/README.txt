# Introdução
API utilizada pelo parceiro Smiles para fazer acúmulo e resgate de milhas na Smiles.

As credenciais *client_id* e *client_secret* devem ser solicitadas para Smiles para acesso ao ambiente de testes. </br>
Demais variáveis como *parceiro*, *productName*, *partnerAlias* também devem ser solicitadas ao seu contato imediato na Smiles. </br>
Segue abaixo as variáveis de ambiente utilizadas nesta documentação para ser importada no Postman. </br>
[Postman Environment](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Smiles-Partner-ENV.postman_environment.json)

# Ambientes
Segue abaixo os ambientes:
* **Homologação:** https://api-{parceiro}-hml.smiles.com.br/
* **Produção:** https://api.smiles.com.br/

# Autenticação
É usada o padrão OAuth para autenticação. A Smiles fornecerá um client_id e um client_secret usada para obter um token "Bearer" e este token será usado para a ivocação de todas as APIs.

# Fluxo para Acúmulo de Milhas
Segue abaixo os fluxos utilizados para fazer um acúmulo de milhas na Smiles.

## Acúmulo de milhas com cadastro
![alt text](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Ac%C3%BAmulo+de+Milhas+com+cadastro.png "Acumulo de milhas com cadastro")
[Clique para ampliar](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Ac%C3%BAmulo+de+Milhas+com+cadastro.png)

## Acúmulo de milhas sem cadastro
![alt text](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Ac%C3%BAmulo+de+Milhas+sem+cadastro.png "Acumulo de milhas sem cadastro")
[Clique para ampliar](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Ac%C3%BAmulo+de+Milhas+sem+cadastro.png)

# Fluxo para Resgate de Milhas
Para realizar o resgate de milhas é necessário autenticação do usuário através do teclado virtual da Smiles. Segue abaixo o link do tutorial: </br>
[Tutorial do teclado virtual Smiles](https://estaticos.smiles.com.br/SmilesKeyboard/index.html) </br></br>
Segue abaixo os fluxos utilizados para fazer um resgate de milhas na Smiles.

## Resgate de milhas simples
![alt text](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Resgate+de+Milhas+-+Simples.png "Resgate de milhas simples")
[Clique para ampliar](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Resgate+de+Milhas+-+Simples.png)

## Resgate de milhas com vários itens
![alt text](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Resgate+de+Milhas+-+V%C3%A1rios+Itens.png "Resgate de milhas multi-itens")
[Clique para ampliar](https://s3.amazonaws.com/estaticos.smiles.com.br/api-doc/Resgate+de+Milhas+-+V%C3%A1rios+Itens.png)