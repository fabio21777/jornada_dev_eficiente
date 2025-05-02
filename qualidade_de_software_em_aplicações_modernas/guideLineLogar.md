# [voltar](guideline.md)

## Guia para logar


### Quando logar e qual nível de severidade usar

1. Sempre que tiver alteração de estado no sistema, realize o log em nível de info antes e depois da realização da alteração do estado.

2. Sempre que for consumir serviços externos, realize o log em nível de info antes e depois da chamada de api.

3. Sempre que você realizar um tratamento de erro, cujo problema permite que o fluxo da aplicação continue, realize o log em nível de error. Lembrando de evitar logar em nível de erro e relançar o problema para cima.

4. Realize log em nível de debug quando o código tiver caminhos de decisão, como ifs, loops etc. Faça isso com parcimônia.

## Como logar?

Todas as aplicações devem realizar o log utilizando a biblioteca padrão da empresa que já obriga a passagem de informações relevantes assim como já serializa o log no formato adequado.
