PJBank é uma [conta digital](https://pjbank.com.br/conta-digital/) para empresas na qual é possível receber com boleto bancário (registrado) e cartão de crédito, fazer pagamentos e transferências e emitir ilimitados cartões corporativos. A vantagem em relação a outros serviços são as [tarifas](https://pjbank.com.br/tarifas) e a integração com ERPs.

Opcionalmente, você pode contratar apenas os serviços de recebimento (boleto e cartão) de forma a receber os créditos em qualquer outra instituição bancária.

Esta documentação o ajudará a integrar os serviços do PJBank com seu sistema usando a API.

## Antes de começar
[Por favor, antes de começar veja este tutorial em vídeo](https://vimeo.com/245197264)


## O que eu posso fazer com esta API?
* Abrir uma conta digital;
* Receber com boleto e cartão de crédito;
* Pagar contas;
* Transferir dinheiro entre contas;
* Emitir cartões corporativos;
* Obter extratos.



## Como ser atendido se eu tiver dúvidas?
* Comercial: `(19) 4009 6830`, `0800 878 7887` ou abra um chamado enviando um e-mail para `atendimento@pjbank.com.br`
* Suporte API: Abra um chamado enviando um e-mail para `api@pjbank.com.br`
* Site: https://pjbank.com.br


## Como funciona a API?

É uma API REST, ou seja, há diversos recursos, cada qual com sua URL. Os recursos podem ser acessados e alterados usando operações padrões do HTTP como `GET` (listar ou exibir), `PUT` (alterar um recurso), `POST` (criar um recurso) e `DELETE` (apagar um recurso).

As principais URLs dos recursos são:
* `/contadigital`
* `/contadigital/{{credencial}}`
* `/contadigital/{{credencial}}/transacoes`
* `/contadigital/{{credencial}}/transacoes/{{id}}`
* `/contadigital/{{credencial}}/transacoes/documentos`
* `/contadigital/{{credencial}}/transacoes/documentos/{{id}}`
* `/contadigital/{{credencial}}/recebimentos/`
* `/contadigital/{{credencial}}/recebimentos/transacoes`
* `/contadigital/{{credencial}}/recebimentos/transacoes/{{id}}`
* `/contadigital/{{credencial}}/administradores`
* `/contadigital/{{credencial}}/administradores/{{email}}`

Assim, para criar uma transação você precisará fazer um POST para `/contadigital/{{credencial}}/transacoes`. E para listar as transações, você deve realizar um `GET` para a mesma URL.


Mais informações: 
* Sobre [API REST clique aqui](https://pt.wikipedia.org/wiki/REST).
* Retornos em JSON codificados com Unicode.
* Datas em formato MM/DD/AAAA.
* Números com “.” como separadores decimais, sem separadores milhares e com o sinal “-” representando valores negativos.



## Há separação entre ambiente de teste e produção?
Sim:
* **Sandbox**: `https://sandbox.pjbank.com.br ` - [Download Postman](https://s3-sa-east-1.amazonaws.com/drive.pjbank.com.br/environments/sandbox.postman_environment.json) 
* **Produção**: `https://api.pjbank.com.br ` - [Download Postman](https://s3-sa-east-1.amazonaws.com/drive.pjbank.com.br/environments/produc%CC%A7a%CC%83o.postman_environment.json)

Você pode importar os arquivos que contém as variáveis de ambiente no Postman em: 

`Options` > `Manage Environments` > `Import`

## O status do HTTP tem significado? 
Sim. É importante uma correta validação deste status considerando que um valor maior ou igual a 300 sempre representa um erro. Os status seguem o padrão do HTTP. Os mais comuns são:
* O status `200` significa processamento realizado com sucesso sem ressalvas;
* O status `201` significa que algo solicitado foi criado com sucesso;
* O status `400` significa que algo fornecido da parte do usuário não corresponde com o esperado;
* O status `401` significa que algo deu errado com as credenciais que foram fornecidas para a API;
* O status `403` significa que algo que você está tentando fazer não está disponível para o seu nível de autorização, ou algum recurso ainda não foi liberado pra você;
* O status `500` significa que alguma validação da parte do servidor não ocorreu como planejado na requisição.