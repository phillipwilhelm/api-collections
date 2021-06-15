## Introdução
Esta é a documentação da API da Pontomais. Ela descreve as funcionalidades e fornece exemplos com o objetivo de servir de guia para o desenvolvimento de integrações com a API da Pontomais, que utiliza o modelo de arquitetura REST.

## Primeiros passos
Para utilização desta API, primeiramente é necessário obter o token de sua base. Para isso, siga os seguintes passos:
1. Acesse https://app.pontomais.com.br/#/acessar;
2. Utilize as credenciais de administrador da empresa para autenticar-se;
3. No menu de navegação no canto esquerdo, clique em Marketplace;
4. Clique em "Saiba mais" dentro da área da "API Pontomais";
5. Realize a contratação da API, caso não tenha feito;
6. Após a contratação, estará disponível o campo "Token público" que contém o token de acesso à API.

## Tipos de dados
Instruções para o preenchimento conforme o tipo do campo:
- **Boolean**: preencha com **true** (para verdadeiro) e **false** (para falso).
- **String**: preencha com caracteres alfanuméricos e/ou especiais.
- **Date**: preencha com uma *String* no formato “YYYY-MM-DD”.
- **Integer**: preencha somente com números.
- **Float**: preencha somente com números de ponto flutuante.
- **Code**: preencha com caracteres alfa numéricos (*String*) que sejam únicos no sistema de origem.
- **Phone**: preencha com uma *String* no formato “(DD) XXXX-XXXX” ou “(DD) XXXXX-XXXX”.
- **Timestamp**: preencha com uma cadeia de caracteres numéricos que representem uma data e horário.
- **Object**: preencha com um objeto. Nesta documentação os dados do tipo *Object* possuem uma tabela específica que determina as características de cada atributo.

## Hierarquia de alocação de colaboradores
- Unidade de Negócio
	- Departamento
		- Equipe
			- Colaborador