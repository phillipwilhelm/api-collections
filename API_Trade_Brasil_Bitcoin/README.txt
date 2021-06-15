## Introdução
Esta documentação possui em detalhes exemplos e dicas para elaboração de ferramentas para te auxiliar na automação de seu trade.

## Testnet
Nossas rotas de testes estão temporariamente fora do ar. Nosso email de suporte (suporte@brasilbitcoin.com.br) está disponível 24h para lhe auxiliar caso não encontre o que precisa nesta documentação.

## Autenticação e Respostas
A chave de autenticação deve ser enviada no cabeçalho da requisição, e as respostas serão devolvidas em JSON.

## Mensagens de Erro
Toda requisição rejeitada pela API irá retornar uma mensagem no seguinte formato:
<pre>{
    "success": false,
    "message": "Mensagem de erro"
}
</pre>

## Limites de Requisições
O limite de requisições é de 60 requisições por minuto para **criação de ordens limitadas**. Para as outras chamadas, o limite é de 1 requisição por segundo.
O parâmetro <code>wait</code>, quando houver refere-se ao tempo em segundos restante para a realização de uma nova chamada.

## Suporte e Sugestões
Você pode pedir ajuda para nosso suporte ou sugerir melhorias da plataforma enviando um email para:
suporte@brasilbitcoin.com.br 24h por dia, 7 dias por semana.