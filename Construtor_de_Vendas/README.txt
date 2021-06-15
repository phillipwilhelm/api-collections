**Descrição**

O Construtor de Vendas é uma solução voltada ao mercado imobiliário e possui integração com os principais ERPs desse mercado. A exemplo:
* SAP
* Sienge

Essas integrações ocorrem por meio de APIs, descritas neste documento. Todas essas integrações poderão e deverão ser testadas em nosso painel CVIO, o link para acesso a resposta da requisição de cada API está respectivamente disposto e os dados para login estão listados no item *headers*, com esses dados você terá acesso a nossas interfaces de integração no nosso ambiente de testes.


**Respostas dos endpoints**

| Code | Description                  |
|----|---------------------------------|
| 200  | Informação foi cadastrada ou atualizada com sucesso. |
| 400  | Algum campo informado esta irregular ou não é válido. |
| 401 | Token não é válido ou expirou. |
| 403  | Acesso negado! |
| 405  | Método não permitido. |
| 406  | CVBI não configurado. |