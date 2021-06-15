A  **Colibri POS API** é uma API Rest para interagir com o [Colibri POS](https://wiki.ncrcolibri.com.br/display/col).

A API fornece acesso aos recursos através de URIs. A API opera sob o protocolo HTTP tornando seu uso fácil por qualquer linguagem de programação ou framework. Para usar a API, sua aplicação deve fazer uma requisição HTTP e analisar a resposta. 

O formato de dados utilizado para entrada/saída é o [JSON](http://pt.wikipedia.org/wiki/JSON). Deve-se enviar no header de todas as requisições `POST` e `PUT` o formato `application/json; charset=utf-8`.

Você pode utilizar os verbos padrões do HTTP de acordo com a ação desejada. 

| Verbo | Geralmente faz o que |
|-|-|
|`GET`| Consulta dados do POS. Não exige corpo da requisição.|
|`PUT`| Atualiza dados. Exige um JSON no corpo da requisição.|
|`POST`| Insere/atualiza dados. Exige um JSON no corpo da requisição.|
|`DELETE`| Apaga dados do POS. Não exige corpo na requisição.|

Na descrição de cada endpoint é informado qual verbo está disponível para o recurso.
</br></br>

## Formato das URIs

As URIs dos endpoints da **Colibri API** seguem a seguinte estrutura:

`[http://[servidor]:[porta]/[versao]/[recurso]/?api_key[&parametro1&parametroN]`

| Elemento | Descrição |
|--------- | --------- |
| **Servidor** | Endereço IP (ou nome da máquina) onde o CIS (Colibri Integration Service) está rodando.| 
| **Porta** | Porta IP onde o CIS está servindo os recursos.|
| **Versão** | A versão atual da API é `v1`.|
| **Recurso** | Consulte a documentação para conhecer os recursos disponíveis.
| **API key** | A chave de API fornecida pelo Market Place.|

**IMPORTANTE:** O parâmetro ``api_key`` é mandatório na maioria dos endpoints, com exceção dos endpoints que somente consultam dados, como os de catálogo.
</br></br>

## API Key
A **API key** (chave da API) é um UUID gerado no Colibri Market Place e que identifica unicamente a solução de um parceiro.

Os endpoints só funcionam se a _chave de API_ da solução parceira está presente na licença do Colibri que desce para o estabelecimento. Se a licença do estabelecimento não contém a chave correta, a solução parceira rodando neste estabelecimento não conseguirá consumir os endpoints que exigem chave. Estes endpoints retornarão erro 404 com a mensagem **Chave de licença não encontrada neste ambiente**.

Para que a _chave de API_ desça na licença da loja deve-se solicitar a sua inclusão à revenda responsável ou à NCR, informando qual é a solução parceira e o nº de série da licença. 

**Nota:** As instruções sobre como gerar uma API Key para sua solução estão disponíveis na documentação do [Colibri Extensions SDK](https://wiki.ncrcolibri.com.br/display/plugin).
</br></br>

## Autenticação

A API suporta somente a autenticação básica usando um token base64 no cabeçalho dos requests conforme mostrado abaixo.

`Authorization: Basic TOKEN==`

TOKEN é um base64('usuario:senha') onde

- ``usuario`` pode ser qualquer texto, não é utilizado pela API.
- ``senha`` é a senha do usuário cadastrado no Colibri que será utilizado pela API.

Todas as linguagens de programação modernas oferecem rotinas para codificação e descodificação de strings em base64.

**Nota:** Para logar no Colibri não é necessário o nome de usuário, utiliza-se somente a senha. Por isso, o dado de usuário dentro do token é irrelevante. Porém, mantivemos a notação tradicional do BasicAuth, utilizando ``usuario:senha``, somente por padronização.
</br></br>

## Formato e codificação do JSON

Em requisições ``POST`` e ``PUT`` que exigem o envio de um JSON no corpo da requisição é necessário informar no header a chave 

``Content-Type:application/json; charset=utf-8``

Esse parâmetro é essencial para que o sistema trate corretamente caracteres acentuados.