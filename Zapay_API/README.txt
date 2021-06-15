A Zapay API (ou zAPI) permite a pesquisa e parcelamento de débitos de veículos, tais como multas, IPVA, seguro obrigatório etc.

## Ambiente de Homologação
Para realizar testes da API utilize a url
https://api.sandbox.usezapay.com.br/ 

## Estados suportados
É possível usar a zAPI para veículos dos seguintes estados:
- Alagoas
- Bahia
- Ceará
- Distrito Federal
- Espírito Santo
- Goiás
- Mato Grosso
- Mato Grosso do Sul
- Minas Gerais
- Paraíba
- Paraná
- Pernambuco
- Piauí
- Rio de Janeiro
- Rio Grande do Norte
- Rio Grande do Sul
- Santa Catarina
- São Paulo

# Overview
A zAPI oferece dois fluxos para o parcelamento de débitos de veículos: com e sem checkout.

O fluxo sem checkout é consistido por três etapas:

* Autenticação
* Pesquisa de débitos
* Confirmação de débitos

Já o fluxo com checkout possui as seguintes etapas:

* Autenticação
* Pesquisa de débitos
* Simulação de parcelamento
* Pagamento de débito
* Registro de URL no webhook

A pesquisa de débitos retorna, além dos débitos do veículo para um dado estado, um protocolo de 8 caracteres. Este protocolo é o identificador da operação, e deve ser fornecido nos métodos seguintes.

# Autenticação
As requisições são autenticadas com JSONWebToken. Cada requisição deve conter o token eu seu cabeçalho, da seguinte maneira:

```
Authorization: JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjoxLCJ1c2VybmFtZSI6ImFtb2VkbyIsImV4cCI6MTU2MjQyMTc1NSwiZW1haWwiOm51bGx9.un3L-hiVI9NVM-Xg_I-dPkvpbsa5DWB00L8c_KTO1ew
```

Atenção: O Token obtido desta maneira expira após 5 minutos! É recomendado gerar um novo a cada requisição, ao invés de manter um token para todo o fluxo.

# Status de um pedido

Os possíveis status de um pedido são:

| Status | Descrição|
| ------ | -------- |
| SEARCH | Pesquisa do veículo concluída com sucesso. |
| SIMULATION | Simulação de parcelamento dos débitos selecionados na pesquisa concluída com sucesso. |
| CHECKOUT_SUCCESS | Transação realizada e pagamento autorizado. Aguarde a emissão dos boletos bancários. |
| VEHICLE_NOT_FOUND | Pesquisa realizada e veículo não encontrado na base do Detran. |
| VEHICLE_WITHOUT_DEBTS | Pesquisa realizada e veículo não possui débitos. |
| SERVICE_UNAVAILABLE | Serviço do Detran indisponível no momento. |
| CHECKOUT_FAIL | Transação realizada e pagamento não autorizado. Verifique os dados do cartão e tente novamente.
| PAYMENT_INITIATED | Transação realizada e pagamento autorizado. Pedido em processo de análise de risco e pagamento de boletos.
| BARCODE_EMITTED | Pedido concluído. Débitos quitados junto ao Detran.




# Erros

A zAPI retorna erros com duas chaves: `error` e `detail`. Alguns poucos retornos podem possuir uma terceira chave chamada  `message`. Os retornos são autoexplicativos. Alguns exemplos são:

| Erro | Detalhes|
| ---- | ------- |
| Veículo não encontrado | Verifique as informações do veículo e tente novamente. |
| DETRAN Indisponível | O sistema do DETRAN está indisponível no momento. Tente novamente em alguns instantes. |
| Estado inválido | Este estado não está na lista de estados disponíveis. |
| Requisição inválida | Parâmetro XXX é obrigatório. |
| Protocolo não encontrado | O protocolo inserido não existe ou está incorreto. |
| Pedido não encontrado | Pedido com esse protocolo não existe. |
| Parcela inválida | A parcela deve ser um valor entre 1 e 12.|
| Gateway Fora do Ar | Gateway de pagamento indisponível no momento. Tente novamente mais tarde. |

# Métodos