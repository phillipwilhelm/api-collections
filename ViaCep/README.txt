# Introduction
What does your API do?

Consulta Códigos de Endereçamento Postal (CEP) do Brasil

# Overview
Things that the developers should know about

Para acessar o webservice, um CEP no formato de {8} dígitos deve ser fornecido, por exemplo: "01001000". 
Após o CEP, deve ser fornecido o tipo de retorno desejado, que deve ser "json", "xml", "piped" ou "querty".

Exemplo de pesquisa por CEP: 
viacep.com.br/ws/01001000/json/

# Authentication
What is the preferred way of using the API?

Não

# Error Codes
What errors and status codes can a user expect?

Quando consultado um CEP de formato inválido, por exemplo: "950100100" (9 dígitos), "95010A10" (alfanumérico), "95010 10" (espaço), o código de retorno da consulta será um 400 (Bad Request). Antes de acessar o webservice, valide o formato do CEP e certifique-se que o mesmo possua {8} dígitos. Exemplo de como validar o formato do CEP em javascript está disponível nos exemplos abaixo.

Quando consultado um CEP de formato válido, porém inexistente, por exemplo: "99999999", o retorno conterá um valor de "erro" igual a "true". Isso significa que o CEP consultado não foi encontrado na base de dados.

# Rate limit
Is there a limit to the number of requests an user can send?

Não